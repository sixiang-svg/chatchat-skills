---
id: docker-patterns
name: Docker Patterns
description: Design efficient Docker build and runtime patterns for secure, reproducible, and deployable containerized applications.
category: Development
requires: ["application runtime stack", "deployment environment", "current dockerfile or container setup"]
examples:
  - "Optimize this Dockerfile for smaller image size and faster CI builds."
  - "Design Docker patterns for a multi-service app with health checks and secure defaults."
---

# Docker Patterns

Apply Docker best practices for build performance, runtime safety, and operational reliability.

## When to Use

- You need to containerize an application or improve existing images.
- Current Docker setup is slow, large, or insecure.

## Workflow

1. Assess runtime needs, dependencies, and deployment constraints.
2. Recommend build pattern (multi-stage, cache strategy, base image choice).
3. Harden runtime config (non-root user, env handling, health checks).
4. Define image tagging, versioning, and rollout practices.
5. Validate with local and CI smoke tests.

## Output

- Docker architecture and build strategy
- Security/performance recommendations
- Validation and rollout checklist
