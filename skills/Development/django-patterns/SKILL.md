---
id: django-patterns
name: Django Patterns
description: Apply Django architecture and implementation patterns for scalable apps with clean models, views, services, and tests.
category: Development
requires: ["django project context", "feature requirements", "model or api changes needed"]
examples:
  - "Design a Django feature using service-layer patterns and clean serializer/view separation."
  - "Refactor this Django app to reduce fat views and improve testability."
---

# Django Patterns

Recommend practical Django patterns that keep code maintainable and production-ready.

## When to Use

- You are building or refactoring Django features.
- You need pattern guidance for models, views, serializers, and services.

## Workflow

1. Analyze domain boundaries and current app/module structure.
2. Propose model and service design for clear responsibilities.
3. Define API/view/serializer boundaries and validation flow.
4. Add query optimization and transaction safety guidance.
5. Provide test strategy for unit, integration, and API layers.

## Output

- Django pattern recommendation set
- Refactor/implementation roadmap
- Performance and testing checklist
