---
id: agent-arch-system-design
name: Agent Arch System Design
description: Design production-grade agent architecture with clear control flow, tool orchestration, memory boundaries, and failure handling.
category: Development
requires: ["system requirements document", "non-functional constraints"]
examples:
  - "Design a multi-agent architecture for customer support with routing, escalation, and auditability."
  - "Propose an agent system design for code generation with tool-use limits and fallback modes."
---

# Agent Arch System Design

Use this skill when planning the architecture of an AI agent system before implementation.

## When to Use

- You need to decide between single-agent vs multi-agent workflows.
- You need safe tool invocation, memory strategy, and observability.
- You need to define latency/cost/reliability trade-offs.

## Design Workflow

1. Define scope: tasks, constraints, and success metrics.
2. Select execution model (single orchestrator, supervisor-worker, specialist agents).
3. Define tool contracts (inputs, outputs, timeouts, retries, budgets).
4. Define memory model (ephemeral context, session memory, long-term store).
5. Add control policies (permission gates, guardrails, escalation paths).
6. Add failure strategy (timeouts, fallback responses, human handoff).
7. Add observability (traces, token usage, tool error taxonomy).
8. Validate with representative scenarios and adversarial cases.

## Output

- Architecture diagram (components + data/control flow)
- Tool and memory boundary specification
- Risk and mitigation checklist
- Rollout plan (pilot -> limited -> full)

- Brief plan or checklist
- Key recommendations and caveats
