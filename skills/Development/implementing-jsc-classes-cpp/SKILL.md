---
id: implementing-jsc-classes-cpp
name: Implementing JSC Classes C++
description: Implement JavaScriptCore-backed classes in C++ with correct bindings, memory management, and runtime behavior.
category: Development
requires: ["jsc class interface definition", "c++ binding source files", "gc/lifecycle constraints"]
examples:
  - "Implement a new JSC class in C++ for this runtime module with property/method bindings."
  - "Review this JSC C++ class implementation for GC safety and exception handling."
---

# Implementing JSC Classes C++

Guide JSC class implementation in C++ with focus on correctness, performance, and maintainability.

## When to Use

- You are exposing native C++ functionality to JavaScriptCore.
- You need safe binding patterns and lifecycle handling.

## Workflow

1. Define JS-facing class surface and native backing model.
2. Implement constructor/method/property bindings.
3. Ensure proper memory ownership and GC interaction.
4. Add error translation and exception-safe behavior.
5. Validate behavior with runtime integration tests.

## Output

- JSC class binding plan
- Memory and lifecycle guidance
- Verification checklist
