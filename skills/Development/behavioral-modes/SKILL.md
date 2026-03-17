---
id: behavioral-modes
name: Behavioral Modes
description: Define execution modes for coding agents to improve reliability, safety, and task-fit behavior.
category: Development
requires: ["agent role description", "task types to support", "risk and safety constraints"]
examples:
  - "Define behavioral modes for our coding assistant: explore, implement, review, and debug."
  - "Given these failure cases, design stricter agent modes with clear transitions and guardrails."
---

# Behavioral Modes

Design explicit operating modes so an agent can adapt behavior to task intent and risk level.

## When to Use

- You are building an agent with mixed responsibilities.
- You need predictable behavior and safe mode switching.

## Workflow

1. Identify task families (planning, implementation, review, debugging).
2. Define each mode's goals, allowed actions, and boundaries.
3. Specify transition rules between modes and escalation triggers.
4. Add safeguards for destructive or high-risk actions.
5. Validate mode design against known failure scenarios.

## Output

- Mode definitions and transition matrix
- Safety guardrails per mode
- Test scenarios for behavior validation
