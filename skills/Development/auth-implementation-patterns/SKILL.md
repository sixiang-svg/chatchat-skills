---
id: auth-implementation-patterns
name: Auth Implementation Patterns
description: Design secure authentication and authorization flows using proven patterns for sessions, tokens, and access control.
category: Development
requires: ["auth requirements", "user role model", "target platform stack"]
examples:
  - "Design auth for a multi-tenant SaaS app with RBAC, refresh tokens, and SSO support."
  - "Given these API routes and roles, propose secure authn/authz patterns and middleware boundaries."
---

# Auth Implementation Patterns

Recommend practical authn/authz implementations that reduce security risk and support scale.

## When to Use

- You need to implement authentication and authorization from scratch.
- You want pattern-level guidance for tokens, sessions, RBAC/ABAC, and identity providers.

## Workflow

1. Model identities, roles, permissions, and trust boundaries.
2. Choose appropriate auth pattern (session, JWT, OAuth/OIDC) based on platform and risk.
3. Define token/session lifecycle, key rotation, and revocation strategy.
4. Design route-level authorization enforcement and policy checks.
5. Add security controls: MFA options, audit logs, brute-force mitigation, and secret handling.

## Output

- Auth architecture recommendation
- Endpoint enforcement plan
- Security checklist and implementation caveats
