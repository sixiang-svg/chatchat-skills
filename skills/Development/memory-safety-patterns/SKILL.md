---
id: memory-safety-patterns
name: Memory Safety Patterns
description: Apply memory safety patterns to prevent leaks, corruption, races, and lifetime bugs in systems-level codebases.
category: Development
requires: ["target language/runtime", "code paths with memory risk", "current memory/ownership model"]
examples:
  - "Review this C++ module for memory safety issues and propose ownership fixes."
  - "Define memory safety patterns for this Rust/C interop boundary."
---

# Memory Safety Patterns

Strengthen memory correctness with explicit ownership, lifecycle, and concurrency-safe patterns.

## When to Use

- You are working in languages/environments prone to memory bugs.
- You need preventive patterns, not just one-off fixes.

## Workflow

1. Identify allocation, ownership, and lifetime boundaries.
2. Apply safe patterns for resource management and deallocation.
3. Audit concurrency interactions for shared-memory hazards.
4. Add tooling checks (sanitizers, static analysis, fuzzing).
5. Define regression tests for previously unsafe paths.

## Output

- Memory safety risk map
- Ownership/lifecycle pattern recommendations
- Tooling and test checklist
