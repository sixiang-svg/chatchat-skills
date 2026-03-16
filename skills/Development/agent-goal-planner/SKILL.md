---
id: agent-goal-planner
name: Agent Goal Planner
description: Turn high-level requests into clear, sequenced goals with dependencies, constraints, and measurable completion criteria.
category: Development
requires: ["project objective", "scope constraints"]
examples:
  - "Break this migration objective into milestones with dependencies and validation criteria."
  - "Convert this vague feature request into an actionable goal tree for engineering execution."
---

# Agent Goal Planner

Use this skill when requirements are broad and need decomposition into executable goals.

## When to Use

- You have a high-level objective but unclear execution path.
- You need explicit sequencing and ownership boundaries.
- You want objective success criteria for each step.

## Planning Workflow

1. Clarify the target outcome and non-goals.
2. Decompose into milestones and tasks.
3. Mark dependencies and prerequisites.
4. Identify risks and unknowns per milestone.
5. Attach validation gates (tests, checks, review criteria).
6. Estimate effort and define done criteria.

## Output

- Goal hierarchy (objective -> milestones -> tasks)
- Dependency graph and critical path
- Success criteria and verification checklist
