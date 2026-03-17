---
id: linkerd-patterns
name: Linkerd Patterns
description: Apply Linkerd operational patterns for secure traffic, reliability tuning, and service-level troubleshooting.
category: DevOps
requires: []
examples:
  - Recommend Linkerd patterns to improve reliability for this microservice stack.
  - Help troubleshoot Linkerd connectivity and latency regressions.
---

# Linkerd Patterns

Use practical Linkerd patterns for resilient and observable service communication.

## When to Use

- You need Linkerd guidance for traffic reliability and policy controls.
- You want safer rollout and failure-handling defaults in service communication.
- You need a troubleshooting flow for Linkerd service behavior.

## Core Patterns

**ServiceProfile for per-route retries/timeouts:** Define retries, timeouts, and routing per route. Without a ServiceProfile, Linkerd uses default timeouts (10s) and no retries.

```yaml
apiVersion: linkerd.io/v1alpha2
kind: ServiceProfile
metadata:
  name: web-svc.default.svc.cluster.local
  namespace: default
spec:
  routes:
  - name: GET /api/users
    condition:
      method: GET
      pathRegex: /api/users
    responseClasses:
    - condition:
        status:
          min: 500
          max: 599
      isFailure: true
    timeout: 5s
    retryBudget:
      retryRatio: 0.2
      minRetriesPerSecond: 10
      ttl: 10s
```

**HTTPRoute for traffic splits:** Use Gateway API HTTPRoute with Linkerd's split backend to canary traffic.

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: reviews-route
spec:
  parentRefs:
  - name: reviews-gateway
  rules:
  - backendRefs:
    - name: reviews-v1
      port: 9080
      weight: 90
    - name: reviews-v2
      port: 9080
      weight: 10
```

**Server and ServerAuthorization for mTLS policy:** Restrict which clients can reach a server. Server defines the port; ServerAuthorization defines allowed clients.

```yaml
apiVersion: policy.linkerd.io/v1beta2
kind: Server
metadata:
  name: reviews-server
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: reviews
  port: 9080
  proxyProtocol: HTTP/1.1
---
apiVersion: policy.linkerd.io/v1beta2
kind: ServerAuthorization
metadata:
  name: reviews-auth
  namespace: default
spec:
  server:
    name: reviews-server
  client:
    meshTLS:
      identities: ["*.default.cluster.local"]
```

**Tap and top for live debugging:** Inspect live traffic and identify latency/error hotspots.

```bash
# Stream live requests for a deployment
linkerd viz tap deploy/reviews -n default

# Top services by RPS and latency
linkerd viz top deploy/reviews -n default

# Tap with method and path
linkerd viz tap deploy/reviews --to deploy/ratings -n default
```

## Reliability Tuning Workflow

1. Identify critical paths and latency-sensitive routes.
2. Create ServiceProfiles for those routes with explicit timeouts and retry budgets.
3. Set retries only for idempotent routes; avoid retries on POST/PUT/DELETE.
4. Tune `retryRatio` and `minRetriesPerSecond` to limit retry amplification.
5. Validate with `linkerd viz tap` and `linkerd viz top` before and after changes.

## Common Pitfalls

- **Retries on non-idempotent routes:** Retrying POST/PUT/DELETE can duplicate side effects; restrict retries to GET and other idempotent methods.
- **Missing ServiceProfile causing default timeouts:** Without a ServiceProfile, Linkerd uses 10s timeout and no retries; add ServiceProfiles for routes that need tuning.
- **Proxy injection annotation missing:** Pods need `linkerd.io/inject: enabled` (or namespace annotation); otherwise they bypass the mesh and skip mTLS/retries.
- **Skipping control plane health checks:** Run `linkerd check` before and after changes; unhealthy control plane leads to unpredictable behavior.

## Workflow

1. Identify critical service paths and latency-sensitive operations.
2. Apply ServiceProfile, Server/ServerAuthorization, and HTTPRoute patterns as needed.
3. Tune retries/timeouts/concurrency via ServiceProfile; validate with tap/top.
4. Run `linkerd check` and validate telemetry by service.
5. Provide targeted remediation for unstable edges.

## Output Format

```markdown
## Pattern Selection
- Reliability pattern: ServiceProfile / HTTPRoute / Server+ServerAuthorization
- Security pattern: ServerAuthorization (mTLS identities)

## ServiceProfile (if applicable)
- Routes: <method + pathRegex>
- Timeout: <duration>
- Retry budget: retryRatio, minRetriesPerSecond, ttl
- Response classes: <failure conditions>

## Tuning Plan
- Retry/timeout settings: <values>
- Load handling: <approach>
- Idempotency check: retries only on GET/safe routes

## CLI Commands
- linkerd viz tap <resource> -n <namespace>
- linkerd viz top <resource> -n <namespace>
- linkerd check

## Troubleshooting Checklist
- [ ] linkerd.io/inject: enabled on pods/namespace
- [ ] linkerd check passes
- [ ] ServiceProfile present for tuned routes
- [ ] Retries restricted to idempotent routes
- [ ] Mitigation validated with tap/top
```

## Constraints

- Do not overuse retries where they amplify load.
- Keep mesh policy changes scoped and reversible.
- Validate improvements with before/after metrics.
- Run `linkerd check` after any mesh or policy change.