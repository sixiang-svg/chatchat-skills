---
id: implementing-new-features
name: Implementing New Features
description: Deliver new product features from requirements to release with clear scope, architecture, testing, and rollout controls.
category: Development
requires: ["feature requirements", "affected codebase modules", "acceptance criteria"]
examples:
  - "Break down and implement this new feature with API, UI, and migration tasks."
  - "Create an incremental rollout plan for this feature with test and rollback checkpoints."
---

# Implementing New Features

Guide feature execution so changes are coherent, testable, and safe to deploy.

## When to Use

- You need to implement a new capability across one or more layers.
- You want a structured approach that reduces integration risk.

## Workflow

1. Clarify feature scope, success criteria, and constraints.
2. Design implementation boundaries and dependency order.
3. Execute in incremental milestones with integration checks.
4. Add unit/integration/e2e validation for behavior and regressions.
5. Define rollout, monitoring, and rollback strategy.

## Output

- Feature implementation roadmap
- Cross-module dependency plan
- Test and rollout checklist
