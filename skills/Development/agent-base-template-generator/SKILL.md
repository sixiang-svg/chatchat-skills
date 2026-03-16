---
id: agent-base-template-generator
name: Agent Base Template Generator
description: Generate a reusable base template for new agents, including instruction scaffolding, tool contracts, and safety defaults.
category: Development
requires: ["agent purpose statement", "tool and runtime constraints"]
examples:
  - "Generate a base template for a research agent that uses web search and citation formatting."
  - "Create an agent starter template for customer support with escalation and compliance sections."
---

# Agent Base Template Generator

Use this skill when creating a standardized starting template for new agents.

## When to Use

- You want consistent structure across many agents.
- You need repeatable defaults for tone, safety, and tool usage.
- You are onboarding teams to build agents quickly with fewer mistakes.

## Template Generation Workflow

1. Capture agent purpose, audience, and boundaries.
2. Define required sections (role, goals, constraints, escalation, output format).
3. Add tool policy blocks (when to call tools, timeouts, retries, no-op conditions).
4. Add safety/compliance defaults (disallowed actions, sensitive data handling).
5. Add examples for successful and failing scenarios.
6. Add a test checklist and launch-readiness criteria.

## Output

- Base template file content
- Required customization points
- Validation checklist for new agents

- Brief plan or checklist
- Key recommendations and caveats
