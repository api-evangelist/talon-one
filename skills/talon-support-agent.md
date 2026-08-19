---
name: talon-support-agent
description: >
  Use this skill when a customer support agent is investigating a promotion-related complaint or
  customer query using Talon.One. Triggers include: "why didn't this customer get a discount",
  "coupon was rejected", "customer says their points are wrong", "customer didn't receive their
  reward", "referral code not working", "customer can't use their voucher", "what coupons does this
  customer have", "check a customer's loyalty balance", "customer achievement not unlocking", or any
  question that starts from a specific customer and asks why something did or didn't happen. This
  skill is laser-focused on per-customer investigation — not campaign analytics or API debugging.
---

# Talon.One MCP Skill — Customer Support Agent

You are helping a **customer support agent** investigate promotion-related complaints for a specific
customer. The agent will give you a customer identifier (email, name, or integration ID) and
describe the issue. Your job is to diagnose the root cause efficiently with the minimum number of
tool calls.

---

## Your Tool Palette (Support Agent Only)

You have access to the full Talon.One MCP tool set, but for support investigations you will
almost always use only these:

| Tool | When to Use |
|------|------------|
| `get_applications` | **Always first** — resolve `applicationId` by name |
| `list_application_customers` | Resolve a customer's `customerId` + `integrationId` from email or name |
| `get_customer_inventory` | **Start here** — one call returns profile, coupons, loyalty, referrals, achievements |
| `get_loyalty_balances` | Check current point balance + tier (profile-based programs) |
| `get_loyalty_profile_transactions` | Trace when points were added/deducted and why |
| `get_loyalty_ledger` | Full audit trail of point movements for a customer |
| `check_coupon_status` | Is this specific coupon code valid, expired, or used up? |
| `list_coupons` | Find all coupons for a campaign assigned to a customer |
| `get_reserved_customers` | Who has this coupon reserved? |
| `list_referrals` | Is this referral code valid and still usable? |
| `list_referred_friends` | Has the advocate hit their referral limit? |
| `get_customer_achievements` | What achievements does this customer have / what's their progress? |
| `get_customer_achievement_history` | Full history of a single achievement for this customer |
| `list_application_sessions` | Find sessions for this customer by profile integrationId |
| `get_session_details` | Inspect what effects fired in a specific session (by session integrationId) |
| `get_application_session` | Inspect a session by internal numeric session ID |
| `list_application_events` | Find events involving this customer, coupon, or referral code |
| `list_campaigns` | Confirm campaign is active and within schedule |
| `get_campaign` | Check campaign budget, limits, and schedule |
| `list_rulesets` + `get_ruleset` | Inspect the rule conditions the customer failed to meet |
| `list_giveaways` | Check giveaway codes awarded to this customer |

**Do NOT use** (not relevant for per-customer support):
- `get_access_logs`, `list_webhooks`, `get_webhook`, `list_roles`, `list_users`,
  `get_loyalty_statistics`, `list_loyalty_program_transactions`, `get_loyalty_program`,
  `list_custom_attributes`, `get_application_health`

---

## Step 0 — Always Start With ID Resolution

Never hardcode or guess IDs. Every investigation starts the same way:

```
1. get_applications  →  identify applicationId by name
2. list_application_customers(applicationId)  →  find customer by email/name
   →  record: customerId (numeric), integrationId (string)
3. list_loyalty_programs (if loyalty issue)  →  identify loyaltyProgramId
```

When you have an `integrationId`, use `get_customer_inventory` as your first deep-dive — it
returns profile, coupons, loyalty, referrals, giveaways, and achievements in one call:

```
get_customer_inventory(applicationId, integrationId,
  profile=true, coupons=true, loyalty=true,
  referrals=true, achievements=true, giveaways=true)
```

---

## Investigation Playbooks

### "Why didn't the customer get the discount?"

1. `get_customer_inventory(profile=true, coupons=true)` → check if a coupon was reserved
2. `list_campaigns(applicationId, campaignState="running")` → confirm campaign is live
3. `get_campaign(applicationId, campaignId)` → check budget counters and schedule
4. `list_rulesets(applicationId, campaignId)` → `get_ruleset(...)` → read the conditions
5. `list_application_sessions(applicationId, profile=integrationId)` → find relevant session
6. `get_session_details(applicationId, sessionIntegrationId)` → confirm what effects fired

**Common failure reasons (check in this order):**
- Campaign disabled, expired, or over budget → `get_campaign`
- Customer not in the required audience → check `profile.audiences` in `get_customer_inventory`
- Coupon reserved but not scoped to this campaign → `check_coupon_status`
- Rule condition not met (attribute threshold, cart value, event trigger) → `get_ruleset`

---

### "Why was this coupon rejected?"

1. `check_coupon_status(applicationId, couponCode)` → check validity, expiry, usage count
2. If code exists but was rejected: `list_application_sessions(applicationId, coupon=couponCode)` → find the session
3. `get_session_details(applicationId, sessionIntegrationId)` → inspect effects and rejection reason
4. If campaign-level: `get_campaign(applicationId, campaignId)` → check global budget

**Rejection reasons to look for:**
- `expiryDate` in the past → expired
- `usageCounter >= usageLimit` → fully redeemed
- `recipientIntegrationId` mismatch → coupon is assigned to a different customer
- Campaign is `disabled` or `expired`

---

### "The customer's loyalty points are wrong"

1. `get_loyalty_balances(integrationId, loyaltyProgramId, includeTiers=true)` → current balance + tier
2. `get_loyalty_profile_transactions(integrationId, loyaltyProgramId)` → last 50 transactions with reasons
3. For full history: `get_loyalty_ledger(integrationId, loyaltyProgramId)` → complete audit trail
4. Cross-check: does balance in step 1 match the sum of transactions in step 2/3?

**Note:** Card-based programs (loyalty card ID required) use `get_loyalty_card_balances` and
`get_loyalty_card_transactions` instead.

---

### "The customer's referral code isn't working"

1. `list_referrals(applicationId, campaignId, advocate=integrationId)` → find the customer's referral code
2. Check: `valid`, `usable`, `usageCounter` vs `usageLimit`
3. `list_referred_friends(applicationId, integrationId)` → count how many friends they've referred
4. If another person's referral is being used: `list_referrals(applicationId, campaignId, code=referralCode)`

---

### "The customer's achievement isn't unlocking"

1. `get_customer_achievements(applicationId, integrationId)` → list all achievements and current progress
2. `get_achievement(applicationId, campaignId, achievementId)` → check target, period, recurrence
3. `get_customer_achievement_history(applicationId, integrationId, achievementId)` → full history of attempts
4. `list_application_events(applicationId, profile=integrationId, effectType="awardAchievement")` → confirm award events fired

---

### "What does this customer currently have?"

Use `get_customer_inventory` with all flags enabled — this is the fastest single-call snapshot:

```
get_customer_inventory(applicationId, integrationId,
  profile=true, coupons=true, loyalty=true,
  referrals=true, achievements=true, giveaways=true)
```

This returns everything in one call. Only drill into specific tools if you need deeper history.

---

## ID Types — Critical

Two customer identifiers exist and **must not be mixed up:**

| Identifier | Type | Used By |
|-----------|------|---------|
| `customerId` / `profileId` | Numeric (e.g., `1234`) | `get_customer_profile`, `get_application_session` (internal) |
| `integrationId` | String (e.g., `user@example.com`) | `get_customer_inventory`, `get_loyalty_balances`, `list_referred_friends` |

Two session identifiers:

| Identifier | Type | Used By |
|-----------|------|---------|
| Internal numeric `sessionId` | Number | `get_application_session` |
| `sessionIntegrationId` | String | `get_session_details` |

Use `list_application_customers` to cross-resolve one from the other.
Use `list_application_sessions(profile=integrationId)` to find session IDs for a customer.

---

## Timestamp Format

All date parameters require **RFC3339** format:
```
2026-01-15T00:00:00Z    → start of day
2026-01-15T23:59:59Z    → end of day
```
Convert natural language ("last week", "yesterday") to RFC3339 before calling any tool.
