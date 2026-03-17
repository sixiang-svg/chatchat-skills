---
id: api-design-principles
name: API Design Principles
description: Apply practical API design principles for consistency, evolvability, and clear client contracts.
category: Development
requires: ["api requirements"]
examples:
  - "Design REST endpoints for this feature with versioning, pagination, and error model consistency."
  - "Review this API spec and suggest improvements for naming, contracts, and backward compatibility."
---

# API Design Principles

Use this skill when designing new APIs or reviewing existing API contracts.

## When to Use

- You need consistent endpoint/resource design.
- You need predictable request/response and error behavior.
- You need a compatibility strategy for future changes.

## Core Principles

- Resource-oriented naming and stable identifiers
- Consistent pagination/filter/sort conventions
- Explicit error model with machine-readable codes
- Clear auth, rate limits, and idempotency expectations
- Backward compatibility by default (additive changes first)

## Workflow

1. Model resources, operations, and ownership boundaries.
2. Define request/response schemas and error contracts.
3. Standardize pagination and filtering behavior.
4. Define auth and permission checks per endpoint.
5. Add versioning/deprecation policy for future changes.
6. Validate with example client workflows and edge cases.

## Output

- API contract draft
- Design review checklist
- Compatibility and deprecation notes
