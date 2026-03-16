---
id: dependency-update
name: Dependency Update
description: Plan and execute safe dependency upgrades with compatibility checks, risk analysis, and rollback readiness.
category: Development
requires: ["dependency manifest file", "target package(s) and version range", "test or build command"]
examples:
  - "Update these npm dependencies to latest safe versions and list breaking-change risks."
  - "Plan a dependency upgrade for this Python project with rollback and verification steps."
---

# Dependency Update

Handle dependency updates in a controlled way that minimizes regressions.

## When to Use

- You need to update one or more dependencies safely.
- You want clear compatibility and testing guidance before merge.

## Workflow

1. Identify current and target versions with changelog review.
2. Classify risk (patch/minor/major and transitive impact).
3. Apply upgrades in coherent groups.
4. Run build/tests and resolve breakages.
5. Document risks, follow-ups, and rollback path.

## Output

- Upgrade plan and grouping strategy
- Compatibility risk notes
- Verification and rollback checklist
