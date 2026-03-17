---
id: frontend-to-backend-requirements
name: Frontend To Backend Requirements
description: Translate frontend feature needs into backend-ready API, validation, and data contract requirements.
category: Development
requires: ["frontend user stories", "ui data flow details", "current backend capabilities"]
examples:
  - "Convert this frontend checkout spec into backend API requirements and payload contracts."
  - "Map frontend filtering/sorting requirements into backend query and pagination specs."
---

# Frontend To Backend Requirements

Bridge frontend intent and backend implementation details with precise, testable contracts.

## When to Use

- Frontend and backend teams need aligned implementation requirements.
- UI requirements are clear but backend contracts are not.

## Workflow

1. Extract frontend interaction and data requirements per screen flow.
2. Define backend endpoints, request/response shapes, and error contracts.
3. Capture auth, authorization, and rate-limit considerations.
4. Specify validation rules, pagination/filtering, and edge-case behavior.
5. Produce acceptance criteria for both FE and BE implementation.

## Output

- API and data contract spec
- FE/BE alignment checklist
- Risk and dependency notes
