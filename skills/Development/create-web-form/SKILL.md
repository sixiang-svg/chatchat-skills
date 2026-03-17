---
id: create-web-form
name: Create Web Form
description: Build robust web forms with schema validation, accessible controls, and reliable submission/error handling.
category: Development
requires: ["form field requirements", "validation rules", "submission endpoint or action"]
examples:
  - "Create a signup form with field-level validation, password rules, and accessible error messages."
  - "Implement a multi-step form for onboarding with save-progress and retry-safe submission."
---

# Create Web Form

Implement forms that users can complete quickly while preventing invalid or unsafe submissions.

## When to Use

- You need to build a new form flow in a web app.
- Existing forms suffer from validation or usability problems.

## Workflow

1. Define required fields, defaults, and conditional sections.
2. Implement client and server validation with actionable messages.
3. Handle submit lifecycle (loading, success, recoverable failure).
4. Add accessibility support for keyboard and screen readers.
5. Cover edge cases with tests and clear retry behavior.

## Output

- Form architecture and validation plan
- Submission/error handling strategy
- Accessibility and test checklist
