---
id: dispatching-parallel-agents
name: Dispatching Parallel Agents
description: Coordinate parallel agent execution with task partitioning, dependency handling, and deterministic result aggregation.
category: Development
requires: ["task breakdown", "parallelization constraints", "merge criteria for outputs"]
examples:
  - "Split this large code audit into parallel agent tasks and define how to merge findings."
  - "Design a parallel agent strategy for generating docs, tests, and refactors safely."
---

# Dispatching Parallel Agents

Use structured orchestration to run independent work in parallel without losing quality or consistency.

## When to Use

- The task has independent subproblems that can run concurrently.
- You need controlled fan-out/fan-in for multi-agent workflows.

## Workflow

1. Partition work into independent, bounded subtasks.
2. Define dependencies and ordering constraints.
3. Set per-agent instructions, context scope, and output contracts.
4. Aggregate outputs with conflict and duplication handling.
5. Validate integrated result against original objective.

## Output

- Parallel execution plan
- Agent task contracts and merge strategy
- Final validation checklist
