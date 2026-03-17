---
id: avalonia-viewmodels-zafiro
name: Avalonia Viewmodels Zafiro
description: Design and implement Zafiro-style Avalonia viewmodels with clear state flow, commands, and testability.
category: Development
requires: ["avalonia view requirements", "ui state and actions", "current viewmodel code (if any)"]
examples:
  - "Create a ViewModel for this checkout screen in Avalonia with commands, validation, and loading states."
  - "Refactor this existing Avalonia ViewModel to follow Zafiro patterns and improve testability."
---

# Avalonia Viewmodels Zafiro

Build maintainable Avalonia viewmodels that separate UI behavior from business logic and are easy to test.

## When to Use

- You need a new ViewModel for an Avalonia screen.
- Existing ViewModels have mixed concerns or hard-to-test logic.

## Workflow

1. Map UI states, user actions, and side effects from the requirements.
2. Define ViewModel properties, commands, and validation rules.
3. Separate domain/service calls from presentation concerns.
4. Add patterns for loading, success, and error state transitions.
5. Propose unit tests for command behavior and state updates.

## Output

- ViewModel structure and responsibilities
- Command and state management plan
- Test checklist and refactor guidance
