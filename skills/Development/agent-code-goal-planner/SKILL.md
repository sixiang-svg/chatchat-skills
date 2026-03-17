---
id: agent-code-goal-planner
name: Agent Code Goal Planner
description: Convert coding requests into a goal-driven implementation plan with milestones, dependencies, and validation checkpoints.
category: Development
requires: ["feature specification", "acceptance criteria"]
examples:
  - "Plan implementation for this auth feature with phased milestones and test gates."
  - "Break this refactor request into executable coding goals with risk checkpoints."
---

# Agent Code Goal Planner

Use this skill to turn ambiguous coding tasks into clear, incremental delivery plans.

## When to Use

- A coding request is large or vague.
- Multiple files/systems are affected and sequencing matters.
- You need explicit verification steps before completion.

## Planning Workflow

1. Clarify objective, constraints, and non-goals.
2. Identify impacted modules and external dependencies.
3. Split work into milestones with measurable outcomes.
4. Define implementation order and rollback points.
5. Attach tests/validation criteria to each milestone.
6. Highlight risks and unknowns with mitigation actions.

## Output

- Goal hierarchy (epic -> milestones -> tasks)
- Dependency map and execution sequence
- Test/verification plan per milestone
- Completion criteria and handoff notes

- Brief plan or checklist
- Key recommendations and caveats
