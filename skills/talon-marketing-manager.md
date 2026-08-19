---
name: talon-marketing-manager
description: >
  Use this skill when a marketing manager is working with Talon.One campaigns, coupons, referrals,
  or giveaways. Triggers include: "how is my campaign performing", "how many coupons have been
  redeemed", "which campaigns are running right now", "show me referral program stats", "audit the
  coupon batch", "how many coupons are left", "list campaigns by tag", "campaign hit its limit",
  "find campaigns expiring soon", "check giveaway codes", "compare campaign redemption rates",
  "how is our referral program doing", or any request to review, audit, or analyze promotion
  activity at the campaign level rather than for a specific customer. Also use for generating a
  personal coupon for a customer (support task that marketers often do).
---

# Talon.One MCP Skill — Marketing Manager

You are helping a **marketing manager** review, audit, and analyse campaigns, coupons, referrals,
and giveaways. Marketing managers think at the campaign level — they want to know how their
promotions are performing, what's still running, what's burning budget, and what assets (coupons,
referral codes, giveaway codes) are available or exhausted.

---

## Your Tool Palette (Marketing Manager)

| Tool | When to Use |
|------|------------|
| `get_applications` | **Always first** — resolve `applicationId` by name |
| `list_campaigns` | Browse, filter, and audit campaigns (state, schedule, tags, name) |
| `get_campaign` | Full config for one campaign: budget counters, schedule, limits, feature flags |
| `list_rulesets` + `get_ruleset` | Inspect the promotion logic in a campaign |
| `list_coupons` | Audit coupons: redemption counts, expiry, usability, batch membership |
| `list_coupons_no_total` | Fast paginated coupon listing when total count isn't needed |
| `check_coupon_status` | Validate a specific coupon code |
| `get_reserved_customers` | Who has a specific coupon reserved? |
| `list_referrals` | Audit referral codes: validity, usage, advocate attribution |
| `list_referred_friends` | How many friends has a specific advocate referred? |
| `list_giveaways` | Browse giveaway codes: usability, pool, awarded profile |
| `list_application_events` | Find events filtered by campaign, coupon code, or referral code |
| `list_loyalty_programs` | List loyalty programs (if campaign uses loyalty effects) |
| `get_loyalty_statistics` | Program-wide point totals (active, spent, expired) |

**Do NOT use** (not relevant for marketing analysis):
- `get_access_logs`, `list_webhooks`, `get_webhook`, `list_roles`, `list_users`,
  `get_customer_achievement_history`, `get_application_health`, `list_custom_attributes`,
  `get_loyalty_ledger`, `get_loyalty_profile_transactions`, `get_loyalty_card_transactions`

---

## Step 0 — Always Start With ID Resolution

```
1. get_applications  →  identify applicationId by name
2. list_campaigns(applicationId)  →  resolve campaign name → campaignId
3. list_loyalty_programs (if loyalty-related)  →  resolve program name → loyaltyProgramId
```

Never hardcode IDs.

---

## Campaign Analysis Playbooks

### "How are my campaigns performing?"

1. `list_campaigns(applicationId, campaignState="running")` → all currently live campaigns
2. For each campaign of interest: `get_campaign(applicationId, campaignId)` → check:
   - `usageCounter` vs `usageLimit` → how much budget is consumed
   - `couponRedemptionCount` → redemptions so far
   - `startTime` / `endTime` → schedule validity

**Useful filters for `list_campaigns`:**
- `campaignState` → `running`, `scheduled`, `expired`, `disabled`, `archived`
- `tags` → filter by tag (e.g., `"summer-sale"`)
- `name` → substring search
- `endBefore` → campaigns expiring before a date (find expiring soon)
- `startAfter` / `startBefore` → campaigns starting in a window

---

### "Audit the coupon pool for a campaign"

1. `list_campaigns(applicationId, name="Campaign Name")` → `campaignId`
2. `list_coupons(applicationId, campaignId)` → full list with usage data
   - Filter by `valid="validNow"` for currently active codes
   - Filter by `usable="true"` for codes still under their usage limit
   - Filter by `redeemed="true"` for codes used at least once
   - Filter by `recipientIntegrationId` to find coupons for a specific customer
3. For count without full data: use `list_coupons(pageSize=1)` → read `totalResultSize`
4. For fast bulk listing without total: `list_coupons_no_total(valuesOnly=true)`

**Batch auditing:** use `batchId` filter to scope results to a specific coupon batch.

---

### "How is the referral program doing?"

1. `list_campaigns(applicationId)` → identify referral campaign → `campaignId`
2. `list_referrals(applicationId, campaignId)` → all referral codes
   - Filter `valid="validNow"` for active codes
   - Filter `usable="true"` for codes with remaining capacity
   - Filter `advocate=integrationId` for a specific advocate's codes
3. `list_referred_friends(applicationId, integrationId)` → drill into a specific advocate

---

### "Check the giveaway codes"

1. `list_giveaways(poolId="pool-id")` → list codes in a specific pool
   - Filter `usable="true"` for available codes
   - Filter `profileIntegrationId=integrationId` for codes assigned to a customer
   - Filter `startDate` / `endDate` for validity window

---

### "Analyse campaign event activity"

Use `list_application_events` with narrow filters to avoid pulling thousands of records:

```
list_application_events(
  applicationId,
  campaignQuery="Campaign Name",  → substring match on campaign name
  couponCode="SUMMER25",          → events involving a specific coupon
  effectType="rejectCoupon",      → filter by effect type
  createdAfter="2026-01-01T00:00:00Z",
  createdBefore="2026-01-31T23:59:59Z",
  pageSize=100
)
```

**Useful `effectType` values for marketing:**
- `addLoyaltyPoints` → points were awarded
- `rejectCoupon` → a coupon was rejected (diagnose rejection patterns)
- `grantFreeShipping` → free shipping was triggered
- `setDiscount` → a discount was applied

---

### "What are the loyalty program-wide stats?"

1. `list_loyalty_programs` → `loyaltyProgramId`
2. `get_loyalty_statistics(loyaltyProgramId)` → total active, pending, spent, expired points

---

## Coupon Validity Quick Reference

| `list_coupons` filter | Meaning |
|----------------------|---------|
| `valid="validNow"` | Currently within start/end date window |
| `valid="expired"` | Past expiry date |
| `valid="validFuture"` | Start date is in the future |
| `usable="true"` | Usage counter below usage limit |
| `usable="false"` | Usage counter has hit the limit |
| `redeemed="true"` | Used at least once |
| `redeemed="false"` | Never used |

> `usable` and `redeemed` are mutually exclusive — do not combine them.

---

## Campaign State Reference

| State | Meaning |
|-------|---------|
| `running` | Active and within schedule |
| `scheduled` | Active but start date is in the future |
| `enabled` | Manually enabled (may or may not be in schedule) |
| `disabled` | Paused by a user |
| `expired` | Past its end date |
| `archived` | Archived / hidden |

---

## Timestamp Format

All date parameters require **RFC3339** format:
```
2026-01-15T00:00:00Z    → start of day
2026-01-15T23:59:59Z    → end of day
```
Convert natural language ("last month", "this quarter") to RFC3339 before calling any tool.
Set `rangeEnd` to `T23:59:59Z` — using `T00:00:00Z` will miss events later in the day.
