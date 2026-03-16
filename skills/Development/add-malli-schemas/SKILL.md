---
id: add-malli-schemas
name: Add Malli Schemas
description: Add or update Malli schemas in Clojure projects with validation coverage, migration safety, and clear contract documentation.
category: Development
requires: ["clojure data shape examples", "validation rules"]
examples:
  - "Add Malli schemas for these request/response maps and include validation examples."
  - "Refactor these Malli schemas safely and note any backward compatibility risks."
---

# Add Malli Schemas

Use this skill when introducing or evolving Malli schemas in a Clojure codebase.

## When to Use

- New API/domain data structures need explicit schema contracts.
- Existing schemas are being extended or tightened.
- You need consistent validation and coercion behavior.

## Workflow

1. Identify domain entities and validation boundaries.
2. Define schema shape and reusable sub-schemas.
3. Add required vs optional keys explicitly.
4. Add custom predicates/constraints where needed.
5. Validate sample payloads (valid + invalid cases).
6. Document coercion expectations and error messages.
7. Check compatibility impact for existing consumers.

## Malli-Specific Checks

- Use consistent key namespaces and naming
- Avoid over-broad `any?` fallbacks
- Keep reusable schemas in shared namespaces
- Include explain output examples for debugging

## Output

- Proposed schema definitions
- Validation examples (pass/fail)
- Compatibility and migration notes
