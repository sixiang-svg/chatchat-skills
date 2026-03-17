---
id: error-handling-patterns
name: Error Handling Patterns
description: Define consistent error handling patterns for services and applications with clear observability and recovery behavior.
category: Development
requires: ["application architecture context", "failure scenarios", "logging/monitoring setup"]
examples:
  - "Create error handling patterns for this API service including retries, fallbacks, and user-safe responses."
  - "Refactor this module to use typed errors and centralized error boundaries."
---

# Error Handling Patterns

Improve system resilience by making failures explicit, actionable, and safe to recover from.

## When to Use

- You need consistent error strategy across modules/services.
- Production failures are hard to diagnose or recover from.

## Workflow

1. Categorize errors (validation, dependency, transient, internal).
2. Define standardized error shapes and propagation rules.
3. Add retry/backoff/circuit-breaker behavior for transient faults.
4. Ensure logs/metrics/traces capture root-cause context.
5. Create test cases for failure paths and recovery actions.

## Output

- Error taxonomy and handling strategy
- Recovery and observability plan
- Failure-path testing checklist
