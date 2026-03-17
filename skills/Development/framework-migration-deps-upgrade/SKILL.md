---
id: framework-migration-deps-upgrade
name: Framework Migration Deps Upgrade
description: Plan and execute framework migrations with dependency upgrades, compatibility checks, and phased rollout safeguards.
category: Development
requires: ["current framework/version", "target framework/version", "project dependency manifest"]
examples:
  - "Plan a migration from Next.js 12 to 14 with dependency upgrades and rollback strategy."
  - "Upgrade this framework and related packages while minimizing breaking changes in CI."
---

# Framework Migration Deps Upgrade

Manage complex framework upgrade work with controlled sequencing and risk reduction.

## When to Use

- You are upgrading a major framework version.
- You need a migration path that includes dependency compatibility and testing.

## Workflow

1. Inventory framework-coupled dependencies and plugins.
2. Identify breaking changes and required code migrations.
3. Sequence upgrades in safe, reviewable phases.
4. Run migration checks, build/tests, and targeted regressions.
5. Define rollback criteria and post-deploy verification.

## Output

- Migration roadmap with phases
- Compatibility and risk report
- Validation and rollback checklist
