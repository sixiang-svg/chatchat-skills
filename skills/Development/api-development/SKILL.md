---
id: api-development
name: API Development
description: Implement production-ready APIs with clear contracts, validation, testing, observability, and safe rollout practices.
category: Development
requires: ["api spec"]
examples:
  - "Implement this API endpoint with validation, error handling, tests, and logging."
  - "Build this CRUD API from spec and include pagination and rate-limiting considerations."
---

# API Development

Use this skill when building backend APIs from requirements or specifications.

## When to Use

- You are implementing new API endpoints.
- You need robust request validation and error handling.
- You need release-safe rollout and monitoring.

## Workflow

1. Translate requirements into endpoint contracts.
2. Implement request validation and schema enforcement.
3. Implement business logic with clear service boundaries.
4. Add error mapping with stable codes/messages.
5. Add auth and rate limiting where required.
6. Write unit/integration/contract tests.
7. Add structured logs, metrics, and tracing.
8. Roll out with canary/feature-flag strategy.

## Output

- Endpoint implementation plan
- Validation/testing checklist
- Rollout and rollback notes
