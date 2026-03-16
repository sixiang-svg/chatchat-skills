---
id: cargo-fuzz
name: Cargo Fuzz
description: Set up and run Rust fuzz testing with cargo-fuzz to find crashes, panics, and parser edge-case vulnerabilities.
category: Development
requires: ["rust crate path", "target function or parser", "sample input corpus (optional)"]
examples:
  - "Configure cargo-fuzz for this Rust parser and generate an initial corpus strategy."
  - "Help me triage this fuzz-discovered crash and propose a safe fix with regression tests."
---

# Cargo Fuzz

Use cargo-fuzz effectively to uncover input-handling bugs and improve Rust code robustness.

## When to Use

- You need to fuzz-test Rust code paths that process untrusted input.
- You found a crash and want reproducible triage and fixes.

## Workflow

1. Identify high-risk targets (parsers, decoders, protocol handlers).
2. Create fuzz target harness with clear entrypoint and constraints.
3. Seed useful corpus and configure sanitizers/timeouts.
4. Reproduce and minimize crashes for deterministic debugging.
5. Propose and validate fixes with regression and property checks.

## Output

- Fuzz target setup plan
- Crash triage notes and fix strategy
- Regression checklist for hardened input handling
