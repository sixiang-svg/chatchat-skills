---
id: uv-global
name: UV Global
description: Step-by-step guidance for using uv to manage global Python tool installations and environments.
category: Research
requires: []
examples:
  - How do I use uv to manage global Python tool installations?
  - Explain the difference between uv tool run and uv tool install.
---

# UV Global

Support uv global workflows with clear steps and best practices.

## Instruction
- Determine if the user needs a persistent tool installation or a one-off execution of a Python package.
- Utilize `uv tool install` to set up persistent, isolated command-line tools with their own environments.
- Use `uv tool run` (equivalent to `npx` or `pipx run`) for temporary execution of tools without permanent installation.
- Manage the global tool list by showing, updating, or uninstalling existing tool environments.
- Explain the mechanism of isolated environments to ensure the user understands why global tools do not conflict with local project dependencies.
- Configure path variables or shell completions to integrate `uv`-managed tools into the user's terminal workflow.

## When to Use
- When installing global developer tools like `black`, `ruff`, or `awscli` while maintaining environment isolation.
- When needing to run a specific Python script or CLI tool once without creating a project-specific virtual environment.
- When upgrading from legacy global `pip` installations to a faster, more reliable tool management system.

## Output
- Step-by-step installation or execution commands using the `uv` tool syntax.
- Summaries of installed tools and their corresponding virtual environment locations.
- Technical precautions regarding path configurations and tool versioning.