---
id: dependency-updater
name: Dependency Updater
description: Automate recurring dependency maintenance workflows with update policies, batching rules, and CI validation gates.
category: Development
requires: ["package manager ecosystem", "update cadence policy", "ci test commands"]
examples:
  - "Set up a weekly dependency updater policy with grouped PRs and strict test gates."
  - "Design dependency automation rules that separate security patches from major upgrades."
---

# Dependency Updater

Define repeatable dependency maintenance automation that balances freshness and stability.

## When to Use

- You want a sustainable, automated dependency update process.
- Manual updates are inconsistent or too time-consuming.

## Workflow

1. Define update cadence and allowed version bump levels.
2. Configure grouping strategy by package type and risk.
3. Set CI gates and auto-merge eligibility criteria.
4. Add security-priority escalation path.
5. Establish reviewer ownership and exception process.

## Output

- Dependency automation policy
- Grouping and gating configuration plan
- Risk controls and exception handling
