---
id: messages
name: Messages
description: Design and implement messaging features with delivery guarantees, ordering semantics, retries, and user-facing reliability.
category: Development
requires: ["messaging use case", "transport/protocol constraints", "delivery and ordering requirements"]
examples:
  - "Design a reliable in-app messaging pipeline with read receipts and retry handling."
  - "Implement backend message delivery rules for this chat feature with ordering guarantees."
---

# Messages

Build messaging systems that are robust under latency, failure, and concurrency conditions.

## When to Use

- You are implementing chat, notifications, or message queues.
- You need clear semantics for delivery, retries, and ordering.

## Workflow

1. Define message lifecycle and delivery expectations.
2. Choose storage/transport strategy based on reliability needs.
3. Implement idempotency, retries, and dead-letter handling.
4. Address ordering and concurrency edge cases.
5. Add observability and failure recovery playbooks.

## Output

- Messaging architecture plan
- Reliability and ordering rules
- Monitoring and test checklist
