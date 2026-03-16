---
id: artifacts-builder
name: Artifacts Builder
description: Define and automate build artifacts for reproducible packaging, versioning, and deployment handoff.
category: Development
requires: ["build output targets", "artifact format requirements", "release version scheme"]
examples:
  - "Set up artifact outputs for this service: Docker image, SBOM, and release tarball with semantic versions."
  - "Design a CI artifact strategy for frontend bundles and backend binaries with retention rules."
---

# Artifacts Builder

Create a consistent artifact pipeline so builds are traceable, reproducible, and deployment-ready.

## When to Use

- You need to formalize what build outputs should be produced.
- You want reliable packaging and release handoff across environments.

## Workflow

1. Map source modules to required artifact types and naming conventions.
2. Define versioning, checksum/signing, and metadata requirements.
3. Design CI steps for build, package, verify, and publish.
4. Specify retention, immutability, and rollback strategy.
5. Document consumer expectations for downstream deployment.

## Output

- Artifact specification
- CI pipeline checklist for artifact generation
- Release and rollback considerations
