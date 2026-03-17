---
id: add-components-to-registry
name: Add Components To Registry
description: Add UI components to a shared registry with naming, versioning, documentation, and compatibility checks.
category: Development
requires: ["component package files", "registry endpoint"]
examples:
  - "Add these React components to our internal registry with docs and semantic versioning."
  - "Prepare this component package for registry publication and include migration notes."
---

# Add Components To Registry

Use this skill when publishing reusable components to a shared component registry/library.

## When to Use

- A new component should be consumable by multiple apps/teams.
- Existing components are being updated and require versioned release notes.
- You need to enforce consistency in API and documentation.

## Workflow

1. Validate component API (props/events/slots) and naming conventions.
2. Ensure accessibility and styling tokens are consistent.
3. Add usage examples and edge-case documentation.
4. Write changelog entry and determine semantic version bump.
5. Run tests/build/package checks.
6. Publish with tags and update registry metadata.
7. Communicate breaking changes and migration instructions if needed.

## Quality Checklist

- API surface is minimal and stable
- Props are typed and documented
- Accessibility baseline is met
- Examples include real usage patterns
- Version bump matches change impact

## Output

- Publish checklist with version recommendation
- Registry entry metadata template
- Migration notes (if breaking changes exist)
