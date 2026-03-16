---
id: create-skill
name: Create Skill
description: Design and author high-quality agent skills with clear triggers, constraints, and output expectations.
category: Development
requires: ["skill goal", "target user prompts", "tooling and constraint requirements"]
examples:
  - "Create a new skill for API debugging with clear activation examples and output format."
  - "Draft a skill that handles changelog generation with strict formatting constraints."
---

# Create Skill

Build reusable skills that are precise enough for reliable activation and execution.

## When to Use

- You are adding a new skill to the repository.
- Existing skill instructions are vague or inconsistent.

## Workflow

1. Define the skill purpose, scope boundaries, and non-goals.
2. Specify required user inputs and clear activation examples.
3. Write deterministic instructions with constraints and edge-case handling.
4. Define expected output structure and quality checks.
5. Validate clarity by testing with realistic prompts.

## Output

- Skill frontmatter and instruction draft
- Example prompts and expected outputs
- Review checklist for quality and consistency
