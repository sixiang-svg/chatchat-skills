---
id: graphql
name: GraphQL
description: Design and implement GraphQL schemas, resolvers, and performance safeguards for production-grade APIs.
category: Development
requires: ["graphql use case requirements", "existing data source schema", "auth and performance constraints"]
examples:
  - "Design GraphQL schema and resolvers for this catalog and filtering use case."
  - "Improve this GraphQL API to avoid N+1 issues and enforce field-level authorization."
---

# GraphQL

Build GraphQL APIs that are expressive for clients and safe for backend operations.

## When to Use

- You are building or evolving a GraphQL API.
- You need schema/resolver guidance with scaling considerations.

## Workflow

1. Define domain types, queries, mutations, and input contracts.
2. Map resolvers to services/data access layers.
3. Add validation, authorization, and error patterns.
4. Optimize with batching/caching and query complexity controls.
5. Provide testing and observability checklist.

## Output

- GraphQL schema and resolver plan
- Performance/security recommendations
- Validation and rollout checklist
