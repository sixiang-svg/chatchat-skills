---
id: android
name: Android
description: Build and improve Android features with modern architecture, lifecycle safety, and release-ready validation.
category: Development
requires: ["android project files", "target sdk requirements"]
examples:
  - "Implement this Android feature using ViewModel + repository pattern and add instrumentation coverage."
  - "Refactor this Android screen for lifecycle safety and improve state handling across config changes."
---

# Android

Use this skill for Android app development tasks from feature implementation to stabilization.

## When to Use

- You are adding or refactoring Android app features.
- You need architecture guidance for maintainable code.
- You want reliable behavior across lifecycle and configuration changes.

## Workflow

1. Clarify feature behavior and UX states.
2. Select architecture boundaries (UI, domain, data layers).
3. Implement with lifecycle-safe components (ViewModel/StateFlow).
4. Handle errors/loading/empty states explicitly.
5. Add tests (unit + UI/instrumentation where needed).
6. Validate performance, permissions, and backward compatibility.

## Output

- Implementation plan with affected modules
- Architecture and state-management recommendations
- Validation checklist (tests, lifecycle, performance)
