---
name: talon-loyalty-manager
description: >
  Use this skill when a loyalty program manager is working with Talon.One loyalty data. Triggers
  include: "how many points does this customer have", "what tier is this customer on", "show me the
  loyalty ledger", "check a loyalty card balance", "how are points being earned", "loyalty program
  stats", "customer should have reached Gold tier", "points are expiring", "pending points",
  "subledger balance", "achievement progress", "show all active loyalty programs", "program-wide
  point activity", "card-based loyalty", or any request about loyalty points, tiers, ledgers,
  transactions, cards, or achievement tracking. Distinct from marketing (campaign-level) and support
  (generic complaint) — this persona operates at the loyalty infrastructure level.
---

# Talon.One MCP Skill — Loyalty Program Manager

You are helping a **loyalty program manager** investigate and monitor loyalty programs, point
balances, transaction histories, tiers, cards, and achievements. This persona operates at the
intersection of per-customer detail and program-wide oversight — they need both granular ledger
views and aggregate program health.

---

## Your Tool Palette (Loyalty Manager)

### Program Discovery
| Tool | When to Use |
|------|------------|
| `get_applications` | **Always first** — resolve `applicationId` |
| `list_loyalty_programs` | **Always second (if loyalty)** — resolve `loyaltyProgramId` by name |
| `get_loyalty_program` | Full program config: tiers, point settings, expiry rules |
| `get_loyalty_statistics` | Program-wide aggregates: active, pending, spent, expired points |

### Profile-Based Loyalty (customer identified by `integrationId`)
| Tool | When to Use |
|------|------------|
| `list_application_customers` | Resolve `integrationId` from email/name |
| `get_loyalty_balances` | Current point balance + tier for a customer |
| `get_loyalty_profile_points` | Individual point entries (active/pending/expired) |
| `get_loyalty_profile_transactions` | Paginated transaction log for a customer |
| `get_loyalty_ledger` | Full chronological ledger (all point movements) |
| `list_loyalty_program_transactions` | All transactions across the entire program |
| `get_customer_inventory` | Quick snapshot including loyalty + profile in one call |

### Card-Based Loyalty (customer identified by `loyaltyCardId`)
| Tool | When to Use |
|------|------------|
| `get_loyalty_card_balances` | Current balance on a specific loyalty card |
| `get_loyalty_card_points` | Individual point entries on a card |
| `get_loyalty_card_transactions` | Transaction history for a card |

### Achievements
| Tool | When to Use |
|------|------------|
| `get_customer_achievements` | All achievements and customer's current progress |
| `get_achievement` | Full configuration: target, period, recurrence |
| `get_customer_achievement_history` | Full attempt history for one achievement |
| `list_application_events` | Find `awardAchievement` / `achievementProgress` events |

### Supporting
| Tool | When to Use |
|------|------------|
| `list_campaigns` | Find loyalty-earning campaigns |
| `get_campaign` | Check if campaign driving loyalty is still active |
| `list_application_events` | Find `addLoyaltyPoints` events for a profile or campaign |

**Do NOT use** (not relevant for loyalty management):
- `get_access_logs`, `list_webhooks`, `get_webhook`, `list_roles`, `list_users`,
  `get_application_health`, `list_custom_attributes`, `check_coupon_status` (unless loyalty-coupon combo),
  `list_coupons`, `list_referrals`, `list_giveaways`

---

## Step 0 — Always Start With ID Resolution

```
1. get_applications               →  applicationId (by name)
2. list_loyalty_programs          →  loyaltyProgramId (by name)
3. list_application_customers     →  customerId + integrationId (by email/name)
```

Know which **program type** you're working with before calling any loyalty tool:
- **Profile-based**: customer identified by `integrationId` → use `get_loyalty_balances`, `get_loyalty_profile_transactions`, `get_loyalty_ledger`
- **Card-based**: customer identified by `loyaltyCardId` → use `get_loyalty_card_balances`, `get_loyalty_card_transactions`

---

## Investigation Playbooks

### "What is this customer's loyalty balance and tier?"

**Profile-based program:**
```
get_loyalty_balances(
  integrationId,
  loyaltyProgramId,
  includeTiers=true,          → includes current tier and points to next tier
  includeProjectedTier=true   → includes projected tier based on active points
)
```
Returns: active points, pending points, spent points, expired points, current tier, points to next tier.

**Card-based program:**
```
get_loyalty_card_balances(loyaltyCardId, loyaltyProgramId)
```

**Quick full snapshot (profile only):**
```
get_customer_inventory(applicationId, integrationId, loyalty=true, profile=true)
```

---

### "Show me this customer's full point transaction history"

**Last 50 transactions (default):**
```
get_loyalty_profile_transactions(integrationId, loyaltyProgramId)
```

**Filter by date range:**
```
get_loyalty_profile_transactions(integrationId, loyaltyProgramId,
  startDate="2026-01-01T00:00:00Z",
  endDate="2026-01-31T23:59:59Z"
)
```

**Filter by origin:**
```
get_loyalty_profile_transactions(integrationId, loyaltyProgramId,
  loyaltyTransactionType="session"   → "manual" | "session" | "import"
)
```

**Full audit trail (ledger view):**
```
get_loyalty_ledger(integrationId, loyaltyProgramId)
```

**Pending-activation points only:**
```
get_loyalty_ledger(integrationId, loyaltyProgramId, awaitsActivation=true)
```

> `get_loyalty_ledger` and `get_loyalty_profile_transactions` cover the same data from different
> angles. The ledger is the canonical audit view; transactions are better for programmatic filtering.

---

### "Show me individual point entries (not just totals)"

**Profile-based:**
```
get_loyalty_profile_points(integrationId, loyaltyProgramId, status="active")
```
Status options: `active` (redeemable), `pending` (future start), `expired`

**Card-based:**
```
get_loyalty_card_points(loyaltyCardId, loyaltyProgramId, status="active")
```

---

### "Why does this customer have fewer points than expected?"

1. `get_loyalty_balances(integrationId, loyaltyProgramId)` → confirm current totals
2. `get_loyalty_profile_transactions(integrationId, loyaltyProgramId)` → look for deductions, expirations
3. `get_loyalty_ledger(integrationId, loyaltyProgramId)` → full audit if above isn't enough
4. `list_application_events(applicationId, profile=integrationId, effectType="addLoyaltyPoints")` → confirm earn events fired
5. Cross-check: did the campaign driving points have issues? `list_campaigns(applicationId)` → `get_campaign`

**Common causes:**
- Points expired (`loyaltyTransactionType` shows `expiry` entries in ledger)
- Points are pending (not yet activated) → check `status="pending"` in `get_loyalty_profile_points`
- Point-earning campaign was disabled or over budget
- Session was closed/cancelled before points were awarded

---

### "What is the program-wide loyalty health?"

1. `list_loyalty_programs` → `loyaltyProgramId`
2. `get_loyalty_statistics(loyaltyProgramId)`:
   - `activePoints` → currently redeemable
   - `pendingPoints` → awaiting activation
   - `spentPoints` → redeemed by customers
   - `expiredPoints` → points that lapsed
3. `list_loyalty_program_transactions(loyaltyProgramId)` → all recent transactions across all profiles

---

### "Check this customer's achievement progress"

1. `get_customer_achievements(applicationId, integrationId)` → all achievements + current progress
   - Filter `currentProgressStatus="inprogress"` for active challenges
   - Filter `currentProgressStatus="completed"` for finished ones
2. `get_achievement(applicationId, campaignId, achievementId)` → the achievement's target and period
3. `get_customer_achievement_history(applicationId, integrationId, achievementId)` → full attempt history
4. `list_application_events(applicationId, profile=integrationId, effectType="awardAchievement")` → confirm awards fired

---

## Subledger Filtering

If the loyalty program uses subledgers (e.g., "store-credit", "miles", "cashback"):

```
get_loyalty_balances(integrationId, loyaltyProgramId,
  subledgerId="miles",    → scope to a specific subledger
  includeTiers=true
)
```

Always use `subledgerId` when the program has multiple subledgers — it significantly improves
response performance and avoids mixing balances from different pools.

---

## Profile-Based vs Card-Based: Quick Decision Guide

```
Does the customer have a loyalty CARD ID (physical or digital card)?
  YES → card-based program → use: get_loyalty_card_balances, get_loyalty_card_transactions, get_loyalty_card_points
  NO  → profile-based program → use: get_loyalty_balances, get_loyalty_profile_transactions, get_loyalty_ledger
```

Verify program type by checking `get_loyalty_program(loyaltyProgramId)` → look for `cardBased: true`.

---

## Timestamp Format

All date parameters require **RFC3339** format:
```
2026-01-15T00:00:00Z    → start of day
2026-01-15T23:59:59Z    → end of day
```
When querying "last 30 days", compute the exact timestamps before calling. Default page size for
transaction tools is 50 — increase `pageSize` (max 1000) when investigating longer windows.
