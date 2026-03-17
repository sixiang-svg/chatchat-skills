---
id: istio-traffic-management
name: Istio Traffic Management
description: Configure and validate Istio traffic management for routing, canary rollouts, fault handling, and progressive delivery.
category: DevOps
requires: []
examples:
  - Create an Istio canary rollout plan for this service.
  - Help debug unexpected Istio routing behavior between service versions.
---

# Istio Traffic Management

Operate Istio routing and resilience controls with safe, measurable rollout patterns.

## When to Use

- You need versioned traffic routing and progressive rollout on Istio.
- You want explicit retry/timeout/circuit-breaker behavior.
- You need to diagnose traffic split or policy mismatch issues.

## Core Resource Patterns

**VirtualService weight-based routing:** Use `http.route.destination` with `weight` to split traffic between subsets. Always pair with a DestinationRule that defines those subsets; otherwise Istio may route randomly or fail.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: reviews
spec:
  hosts:
  - reviews
  http:
  - route:
    - destination:
        host: reviews
        subset: v1
      weight: 90
    - destination:
        host: reviews
        subset: v2
      weight: 10
```

**DestinationRule subsets with labels:** Subsets must match pod labels. Define them explicitly so VirtualService routing works predictably.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: reviews
spec:
  host: reviews
  trafficPolicy:
    connectionPool:
      tcp: { maxConnections: 100 }
      http: { http1MaxPendingRequests: 50, http2MaxRequests: 100 }
    outlierDetection:
      consecutive5xxErrors: 5
      interval: 30s
      baseEjectionTime: 30s
  subsets:
  - name: v1
    labels: { version: v1 }
  - name: v2
    labels: { version: v2 }
```

**Fault injection for testing:** Use `http.fault` to simulate delays or aborts. Apply only in test/staging or behind feature flags.

```yaml
http:
- fault:
    delay:
      percentage: { value: 10 }
      fixedDelay: 5s
    abort:
      percentage: { value: 5 }
      httpStatus: 503
  route:
  - destination: { host: reviews, subset: v1 }
```

**Mirror traffic for shadow testing:** Send a copy of traffic to a canary without affecting user responses.

```yaml
http:
- route:
  - destination: { host: reviews, subset: v1 }
  mirror:
    host: reviews
    subset: v2
  mirrorPercentage: { value: 100 }
```

## Progressive Delivery Workflow

Use staged traffic shifts with SLO gates: 5% -> 25% -> 50% -> 100%. At each stage, verify error rate and latency before advancing. If SLO degrades, roll back by setting canary weight to 0 and baseline to 100. Gate criteria: error rate below threshold (e.g., 0.1%), p99 latency within budget, no increase in 5xx.

## Retry, Timeout, and Circuit-Breaker

**Retries:** Set `retries.attempts`, `perTryTimeout`, and `retryOn` (e.g., `5xx,reset,connect-failure`). Avoid retrying non-idempotent methods; retries amplify load on failing backends.

**Timeouts:** Set `timeout` per route. Default is 15s; tune per service. Shorter timeouts reduce cascading failures.

**Circuit-breaker:** Configure via DestinationRule `outlierDetection`. `consecutive5xxErrors` or `consecutiveGatewayErrors` trigger ejection. Use `baseEjectionTime` and `maxEjectionPercent` to limit blast radius.

## Common Pitfalls

- **Missing DestinationRule:** VirtualService subsets reference subsets that do not exist; routing becomes unpredictable or fails.
- **Retries amplifying load:** Retries on failing backends multiply request volume; use `perTryTimeout` and limit `attempts`.
- **Conflict between VirtualServices:** Multiple VirtualServices for the same host can overlap; Istio merges by precedence; document and order rules clearly.
- **Forgetting to create subsets:** DestinationRule must define every subset referenced in VirtualService routes.
- **mTLS mode mismatch:** PeerAuthentication `STRICT` with DestinationRule `DISABLE` (or vice versa) causes connection failures; align modes across namespace and workload.

## Workflow

1. Confirm service versions and desired traffic distribution.
2. Define DestinationRule with subsets and resilience (connectionPool, outlierDetection).
3. Define VirtualService with weight-based routing, retries, timeouts.
4. Run staged traffic shifts (5%->25%->50%->100%) with SLO verification at each step.
5. Capture rollback conditions and action steps.

## Output Format

```markdown
## Traffic Strategy
- Baseline version: <version>
- Candidate version: <version>
- Traffic split plan: 5% -> 25% -> 50% -> 100% (with SLO gates)

## DestinationRule
- Subsets: <list with labels>
- Connection pool: <values>
- Outlier detection: <values>

## VirtualService
- Weight routing: <stages>
- Retries: attempts=<n>, perTryTimeout=<duration>, retryOn=<conditions>
- Timeout: <duration>
- Fault injection / mirror: <if applicable>

## Verification
- [ ] DestinationRule subsets match pod labels
- [ ] Route distribution matches target
- [ ] Error/latency within SLO
- [ ] mTLS mode aligned
- [ ] Rollback path validated
```

## Constraints

- Favor incremental traffic shifts over abrupt cutovers.
- Tie rollout progression to observed SLO behavior.
- Keep rollback instructions explicit and immediate.
- Always define DestinationRule before or with VirtualService.