---
id: api-patterns
name: API Patterns
description: Apply proven API implementation patterns for pagination, idempotency, versioning, consistency, and operational reliability.
category: Development
requires: ["api context"]
examples:
  - "Apply API patterns to this service: idempotency keys, pagination, and standardized errors."
  - "Recommend API patterns for long-running operations and async status polling."
---

# API Patterns

Use this skill when selecting implementation patterns for robust APIs.

## When to Use

- You need consistency across multiple endpoints/services.
- You are deciding between sync vs async endpoint patterns.
- You need a reusable API pattern library for the team.

## Pattern Areas

- Pagination (cursor vs offset)
- Idempotency for mutating operations
- Async jobs (`POST` + status endpoint)
- Versioning and compatibility
- Error response standardization
- Rate limiting and backoff guidance

## Workflow

1. Identify endpoint categories and traffic characteristics.
2. Choose pattern per category and justify trade-offs.
3. Define shared conventions (headers, errors, metadata).
4. Add code-level guardrails and tests for consistency.
5. Document examples for future endpoint authors.

## Output

- Pattern decision matrix
- Standardized API conventions
- Endpoint archetype examples
