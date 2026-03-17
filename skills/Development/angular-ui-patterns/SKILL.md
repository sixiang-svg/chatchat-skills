---
id: angular-ui-patterns
name: Angular UI Patterns
description: Apply Angular UI patterns for scalable component design, state flow, accessibility, and maintainable styling.
category: Development
requires: ["angular component files", "design system guidelines"]
examples:
  - "Refactor this Angular feature into reusable presentational/container components with clear inputs/outputs."
  - "Apply Angular UI best practices to this form screen, including validation states and accessibility."
---

# Angular UI Patterns

Use this skill when designing or refactoring Angular UI code for clarity, reuse, and consistency.

## When to Use

- Components are tightly coupled or hard to test.
- UI state handling is inconsistent across screens.
- You need patterns for forms, layout, and reusable components.

## Workflow

1. Separate presentational and container responsibilities.
2. Define strict component API (`@Input`/`@Output` contracts).
3. Keep side effects in services/effects, not templates.
4. Standardize form validation, error display, and loading states.
5. Enforce accessibility basics (labels, keyboard flow, aria attributes).
6. Use consistent styling strategy and shared UI primitives.

## Output

- Component restructuring plan
- UI state and data-flow recommendations
- Accessibility and consistency checklist
