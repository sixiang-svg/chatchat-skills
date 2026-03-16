---
id: backend-dev-guidelines
name: Backend Dev Guidelines
description: Establish practical backend engineering guidelines for APIs, data changes, testing, observability, and safe releases.
category: Development
requires: ["team backend stack", "current engineering pain points", "service codebase context"]
examples:
  - "Create backend development guidelines for our Node.js services with standards for APIs, tests, and observability."
  - "Given these recurring incidents, define coding and release guidelines to reduce regressions."
---

# Backend Dev Guidelines

Define standards that make backend delivery consistent, reliable, and easier to review.

## When to Use

- Your team needs shared backend conventions.
- Quality and release outcomes vary across services or contributors.

## Workflow

1. Identify stack-specific conventions (API design, error handling, data access).
2. Define minimum testing expectations by change type.
3. Specify migration safety rules and backward-compatibility policy.
4. Set observability standards (logs, metrics, traces, alerts).
5. Add review checklist items and release readiness gates.

## Output

- Backend guideline document outline
- Enforceable checklist for PR reviews
- Rollout plan for team adoption
