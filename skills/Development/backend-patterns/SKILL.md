---
id: backend-patterns
name: Backend Patterns
description: Apply proven backend design patterns for services, data access, reliability, and maintainable code structure.
category: Development
requires: ["backend use case", "current service architecture", "data consistency requirements"]
examples:
  - "For this order service, recommend backend patterns for transactional writes, async events, and retries."
  - "Given our current monolith, suggest backend patterns to improve modularity without a full rewrite."
---

# Backend Patterns

Choose backend patterns that fit current constraints and reduce implementation risk.

## When to Use

- You need practical backend pattern guidance for a specific feature/system.
- You want tradeoff-aware recommendations tied to real constraints.

## Workflow

1. Clarify the use case, data consistency, and latency constraints.
2. Evaluate suitable patterns (layered, repository, CQRS, event-driven, saga).
3. Map each pattern to implementation boundaries and ownership.
4. Identify failure modes and mitigation patterns (timeouts, retries, idempotency).
5. Recommend a phased adoption path to avoid large risky rewrites.

## Output

- Pattern recommendation with rationale
- Integration and migration notes
- Risk checklist and validation steps
