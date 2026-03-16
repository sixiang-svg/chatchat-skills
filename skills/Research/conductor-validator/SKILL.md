---
id: conductor-validator
name: Conductor Validator
description: Validates Conductor project artifacts for completeness and consistency to verify project context before implementation.
category: Research
requires: []
examples:
  - Validate my Conductor project artifacts for consistency.
  - Check the conductor directory for required index and product files.
---

# Check if conductor directory exists
ls -la conductor/

# Find all track directories
ls -la conductor/tracks/

# Check for required files
ls conductor/index.md conductor/product.md conductor/tech-stack.md conductor/workflow.md conductor/tracks.md


## Use this skill when

- Working on check if conductor directory exists tasks or workflows
- Needing guidance, best practices, or checklists for check if conductor directory exists

## Do not use this skill when

- The task is unrelated to check if conductor directory exists
- You need a different domain or tool outside this scope

## Instructions

- Clarify goals, constraints, and required inputs.
- Apply relevant best practices and validate outcomes.
- Provide actionable steps and verification.
- If detailed examples are required, open `resources/implementation-playbook.md`.

## Output
Your response must be structured to provide a project validation report:

### 1. Structure & Artifact Assessment
- **Directory Audit**: A summary of existing vs. missing required files in the `conductor/` path.
- **Track Identification**: A list of detected tracks and their corresponding IDs.

### 2. Validation Logic (Natural Language)
- **Consistency Checks**: A natural language description of the verification steps performed on the project index and plans.
- **Pattern Matching Results**: Feedback on whether the status markers and ID formats comply with the project standards.

### 3. Actionable Checklist & Verification
- **Gap Analysis**: A prioritized list of steps required to bring the project context to a "Ready" state.
- **Best Practices**: Advice on maintaining artifact consistency throughout the project lifecycle.