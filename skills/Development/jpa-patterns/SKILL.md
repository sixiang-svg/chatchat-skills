---
id: jpa-patterns
name: JPA Patterns
description: Apply JPA and Hibernate patterns for entity modeling, query efficiency, transactional integrity, and maintainable persistence layers.
category: Development
requires: ["jpa entity model", "repository/query requirements", "database constraints/indexing context"]
examples:
  - "Refactor these JPA entities and repositories to reduce N+1 queries and improve transaction boundaries."
  - "Design JPA mappings for this domain while preserving cascade and fetch safety."
---

# JPA Patterns

Provide practical JPA guidance to keep persistence logic performant and predictable.

## When to Use

- You are building or tuning Java persistence layers with JPA/Hibernate.
- You need help with entity mapping, queries, and transaction behavior.

## Workflow

1. Review entity boundaries, relationships, and ownership.
2. Define fetch strategies and avoid N+1 query pitfalls.
3. Align repository/query patterns with use-case access paths.
4. Validate transaction scope and consistency requirements.
5. Add testing strategy for persistence behavior and migrations.

## Output

- JPA mapping and repository plan
- Performance and consistency recommendations
- Persistence test checklist
