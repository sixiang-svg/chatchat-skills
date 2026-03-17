---
id: add-reward
name: Add Reward
description: Add a reward mechanism safely by defining rules, eligibility logic, abuse controls, and payout accounting.
category: Development
requires: ["reward logic spec", "existing reward model code"]
examples:
  - "Add a points-based reward flow to this app with eligibility checks and anti-abuse limits."
  - "Implement referral rewards and include expiration, reversal, and audit logging rules."
---

# Add Reward

Use this skill when implementing or extending reward logic (points, credits, referral bonuses, streaks, cashback, etc.).

## When to Use

- A feature requires users to earn points/credits/bonuses.
- You need clear eligibility and payout rules.
- You want safe handling of fraud, reversal, and accounting edge cases.

## Workflow

1. Define reward objective and behavior (what action is rewarded and why).
2. Specify eligibility rules (new user only, region, plan tier, cooldown window).
3. Define calculation logic (fixed amount, percentage, caps, tier multipliers).
4. Add anti-abuse controls (rate limits, device/account checks, duplicate prevention).
5. Implement idempotent reward issuance with unique event keys.
6. Add reversal/void logic for refunds, chargebacks, or policy violations.
7. Log all reward events for auditability.
8. Add tests for happy path, edge cases, and abuse scenarios.

## Output

- Reward rule specification (eligibility, calculation, caps, expiry)
- Implementation checklist (data model + service + tests)
- Risk notes (abuse vectors, rollback/reconciliation approach)

- Brief plan or checklist
- Key recommendations and caveats
