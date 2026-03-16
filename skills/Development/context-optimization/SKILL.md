---
id: context-optimization
name: Context Optimization
description: Optimize context passed to coding agents by selecting relevant files, constraints, and task goals with minimal noise.
category: Development
requires: ["task objective", "candidate file list or paths", "hard constraints and acceptance criteria"]
examples:
  - "Optimize the context for this bugfix task so the agent only gets relevant files and requirements."
  - "Create a context pack for implementing this feature without exceeding token limits."
---

# Context Optimization

Prepare high-signal context bundles that improve agent accuracy and reduce irrelevant processing.

## When to Use

- Agent outputs are noisy or off-target due to poor context.
- You need to stay within context limits while preserving key details.

## Workflow

1. Clarify task outcome and must-follow constraints.
2. Rank files and docs by direct relevance to the task.
3. Remove redundant or low-signal context.
4. Add concise task framing and expected output format.
5. Validate that context still supports end-to-end execution.

## Output

- Curated context pack
- Inclusion/exclusion rationale
- Risk notes for missing information
