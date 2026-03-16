---
id: idapython
name: Idapython
description: Automate reverse engineering workflows in IDA using IDAPython for analysis, renaming, and pattern extraction.
category: Development
requires: ["ida .i64/.idb database path", "target function/address range", "script output format requirements"]
examples:
  - "Write an IDAPython script to rename functions based on this pattern and export call graph data."
  - "Automate string cross-reference analysis for this binary using IDAPython."
---

# Idapython

Use IDAPython scripts to make reverse engineering workflows repeatable and faster.

## When to Use

- You need automation inside IDA for repetitive analysis tasks.
- You want scriptable extraction or transformation of analysis data.

## Workflow

1. Define analysis target and expected output artifacts.
2. Inspect available IDA APIs and object model for the task.
3. Implement script with safe iteration and filtering logic.
4. Validate script results against manual spot checks.
5. Add reuse notes and parameterization.

## Output

- IDAPython script strategy
- API usage and implementation notes
- Verification checklist
