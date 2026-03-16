---
id: c-pro
name: C Pro
description: Develop and review robust C code with attention to memory correctness, portability, and low-level performance.
category: Development
requires: ["c source files", "target platform/compiler", "feature or bug objective"]
examples:
  - "Review this C module for memory safety and undefined behavior, then suggest fixes."
  - "Implement this low-level feature in C with portability across Linux and embedded targets."
---

# C Pro

Guide C development with practical patterns for correctness and maintainability in systems-level code.

## When to Use

- You are writing or debugging systems-level C code.
- You need help with pointers, memory, build portability, or performance.

## Workflow

1. Understand target environment and compiler constraints.
2. Define data structures and interfaces with clear ownership.
3. Implement logic with defensive checks and error propagation.
4. Audit for memory safety, overflow, and undefined behavior.
5. Add tests and tooling guidance (sanitizers/static analysis).

## Output

- C implementation and safety plan
- Portability and performance notes
- Validation checklist
