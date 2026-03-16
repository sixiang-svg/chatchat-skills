---
id: api-integration-specialist
name: API Integration Specialist
description: Integrate external APIs reliably with auth handling, retries, mapping, failure recovery, and monitoring.
category: Development
requires: ["integration target api docs"]
examples:
  - "Integrate this payment API with OAuth2, retries, and idempotent request handling."
  - "Map this third-party API response to our domain model and handle partial failures safely."
---

# API Integration Specialist

Use this skill when connecting your system to third-party or partner APIs.

## When to Use

- You need to consume an external API in production.
- You need robust retry/fallback behavior.
- You need clean mapping between external and internal models.

## Workflow

1. Review provider docs (auth, quotas, errors, webhooks).
2. Define integration boundary and adapter layer.
3. Implement auth/token refresh and secret handling.
4. Add retries, timeout, and circuit breaker policies.
5. Normalize responses into internal DTO/domain models.
6. Add idempotency and duplicate event handling.
7. Add observability and integration health checks.
8. Document failure/replay runbook.

## Output

- Integration design with adapter contract
- Error/retry policy matrix
- Monitoring and incident response checklist
