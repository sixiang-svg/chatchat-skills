---
id: antigravity-workflows
name: Antigravity Workflows
description: Design resilient async workflows that stay reliable under load using retries, backpressure, idempotency, and dead-letter handling.
category: Development
requires: ["workflow requirements"]
examples:
  - "Design an async processing workflow for webhooks with retries, idempotency keys, and DLQ handling."
  - "Refactor this queue-based pipeline to handle spikes without timeouts or duplicate side effects."
---

# Antigravity Workflows

Use this skill for event-driven or queue-based workflows that must remain stable during failures and traffic spikes.

## When to Use

- You are building async/background job systems.
- You need stronger failure recovery and replay safety.
- You want to prevent cascading failures when dependencies degrade.

## Workflow

1. Define workflow stages and ownership boundaries.
2. Add idempotency at every side-effecting step.
3. Implement retries with exponential backoff and jitter.
4. Add circuit breakers and timeout policies for external calls.
5. Introduce backpressure controls (queue limits, concurrency caps).
6. Route poison messages to a dead-letter queue.
7. Add replay and reconciliation procedures.
8. Instrument success/failure/latency metrics per stage.

## Output

- Reliability-oriented workflow design
- Failure mode matrix with mitigation strategy
- Operational runbook (alerts, replay, recovery)
