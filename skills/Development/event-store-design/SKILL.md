---
id: event-store-design
name: Event Store Design
description: Design event stores for event-sourced systems with append-only integrity, replayability, and projection support.
category: Development
requires: ["domain event model", "consistency and ordering requirements", "storage platform constraints"]
examples:
  - "Design an event store schema for this order lifecycle with snapshots and projection rebuilds."
  - "Review this event-sourcing design for idempotency, versioning, and retention."
---

# Event Store Design

Build event-store architectures that preserve history and support safe evolution over time.

## When to Use

- You are implementing or scaling an event-sourced system.
- You need robust event schema, versioning, and replay strategy.

## Workflow

1. Define aggregate boundaries and event ordering semantics.
2. Specify event envelope, metadata, and versioning approach.
3. Design stream partitioning, snapshots, and retention policy.
4. Plan projection rebuild and backfill workflows.
5. Add operational safeguards for duplicates and replay safety.

## Output

- Event store schema and stream strategy
- Versioning and projection guidance
- Reliability and operations checklist
