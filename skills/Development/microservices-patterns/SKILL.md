---
id: microservices-patterns
name: Microservices Patterns
description: Apply microservices architecture patterns for service boundaries, communication, resilience, and operational scalability.
category: Development
requires: ["domain/service boundaries", "traffic and reliability requirements", "current deployment topology"]
examples:
  - "Design microservice boundaries for this ecommerce platform with async event integration."
  - "Recommend resilience patterns for inter-service communication and failure isolation."
---

# Microservices Patterns

Guide microservices design and implementation with tradeoff-aware, operations-ready patterns.

## When to Use

- You are splitting or evolving services in a distributed architecture.
- You need patterns for communication, consistency, and observability.

## Workflow

1. Define service ownership and domain boundaries.
2. Select communication patterns (sync/async) per workflow.
3. Add resilience controls (timeouts, retries, circuit breakers).
4. Design data consistency strategy and failure recovery.
5. Establish observability and deployment guardrails.

## Output

- Microservices architecture recommendations
- Reliability and consistency strategy
- Operational readiness checklist
