---
id: agent-collective-intelligence-coordinator
name: Agent Collective Intelligence Coordinator
description: Coordinate multi-agent collaboration by assigning roles, synthesizing outputs, resolving conflicts, and producing a single coherent final decision.
category: Development
requires: ["multi-agent task brief", "agent role definitions"]
examples:
  - "Coordinate 4 specialist agents to design this feature and synthesize one final technical plan."
  - "Combine outputs from research, architecture, and QA agents into one conflict-resolved recommendation."
---

# Agent Collective Intelligence Coordinator

Use this skill when multiple agents are working on the same problem and you need coherent orchestration.

## When to Use

- Several agents produce overlapping or conflicting outputs.
- You need role assignment, sequencing, and output consolidation.
- You want a final answer with explicit rationale and trade-offs.

## Coordination Workflow

1. Define the objective and decision criteria.
2. Assign distinct roles to agents (research, implementation, risk, review).
3. Set clear output contracts for each role.
4. Run work in parallel where independent; serialize where dependent.
5. Collect outputs and detect contradictions.
6. Resolve conflicts using evidence, constraints, and priorities.
7. Produce one unified recommendation with action steps.

## Output

- Role/task matrix for participating agents
- Consolidated findings and conflict resolution notes
- Final decision with alternatives and confidence level
