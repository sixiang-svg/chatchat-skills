---
id: architecture-patterns
name: Architecture Patterns
description: Recommend architecture patterns based on system constraints, scalability goals, and operational requirements.
category: Development
requires: ["system context", "quality attribute priorities", "deployment constraints"]
examples:
  - "Given this SaaS backend context and reliability goals, recommend suitable architecture patterns and tradeoffs."
  - "Compare modular monolith, microservices, and event-driven options for this workload and team size."
---

# Architecture Patterns

Select and justify architecture patterns that best match the system and team constraints.

## When to Use

- You need to choose between competing architecture approaches.
- You want explicit tradeoff analysis tied to requirements.

## Workflow

1. Clarify scale, latency, consistency, and team ownership constraints.
2. Evaluate candidate patterns against quality attributes.
3. Identify integration boundaries and data ownership model.
4. Highlight migration complexity, failure modes, and observability needs.
5. Recommend a primary pattern and fallback options.

## Output

- Pattern recommendation with rationale
- Tradeoff matrix and risk notes
- Adoption roadmap and guardrails
