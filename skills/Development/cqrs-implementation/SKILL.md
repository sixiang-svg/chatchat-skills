---
id: cqrs-implementation
name: CQRS Implementation
description: Design and implement CQRS patterns for systems needing separated read/write models, scalability, and clear consistency tradeoffs.
category: Development
requires: ["domain use case", "command/write workflows", "query/read requirements"]
examples:
  - "Design a CQRS approach for order management with separate read models and event-driven projections."
  - "Evaluate whether this feature should use CQRS and provide an incremental adoption plan."
---

# CQRS Implementation

Apply CQRS where it provides clear benefits and avoid unnecessary architectural complexity.

## When to Use

- You have divergent read vs write scaling or model needs.
- You need explicit handling of eventual consistency and projections.

## Workflow

1. Identify domain boundaries and command/query separation points.
2. Define write model invariants and command handlers.
3. Design read models, projections, and update pipelines.
4. Plan consistency, retries, idempotency, and failure recovery.
5. Provide migration strategy from current architecture.

## Output

- CQRS suitability assessment
- Command/read model design
- Consistency and rollout checklist
