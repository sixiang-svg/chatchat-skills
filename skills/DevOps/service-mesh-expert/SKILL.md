---
id: service-mesh-expert
name: Service Mesh Expert
description: Design and troubleshoot service mesh architectures for secure service-to-service communication, traffic policy, and operational resilience.
category: DevOps
requires: []
examples:
  - Propose a service mesh architecture for secure east-west traffic.
  - Help troubleshoot service-to-service latency and retries in our mesh.
---

# Service Mesh Expert

Plan, operate, and debug service mesh deployments with clear policy and reliability outcomes.

## When to Use

- You are introducing or scaling a service mesh.
- You need secure, observable service-to-service communication controls.
- You need to diagnose mesh-level routing, mTLS, or resilience issues.

## Mesh-Agnostic Architecture Guidance

**Sidecar vs ambient/sidecarless:** Sidecar proxies give per-pod control and full L7 visibility but add CPU/memory overhead and latency. Ambient or sidecarless modes (e.g., Istio ambient, Cilium) reduce resource cost and simplify rollout but may limit per-workload policy granularity. Choose sidecar when you need fine-grained policy per pod; choose ambient when you prioritize lower overhead and simpler operations.

**Control plane HA:** Run multiple control plane replicas across availability zones. Use leader election or active-passive where supported. Ensure etcd or backing stores are clustered and backed up. Validate failover behavior before production.

**Data plane overhead measurement:** Baseline CPU and memory per pod before mesh injection. After rollout, measure delta per sidecar (typically 50-200 mCPU and 128-256 MiB per proxy). Use resource requests/limits and consider HPA for proxies if they become hot paths.

## mTLS Policy Design

**Strict vs permissive rollout:** Start with permissive mode (accept both mTLS and plaintext) to validate connectivity. Gradually move to strict mode namespace-by-namespace or workload-by-workload. Use `PeerAuthentication` with `PERMISSIVE` first, then `STRICT` after validation. Never flip mesh-wide strict in one change.

**Certificate rotation:** Align rotation windows with your CA's validity. Test rotation in staging; ensure workloads pick up new certs without downtime. Monitor for cert expiry alerts and automate renewal where possible.

## Authorization Policy Patterns

**Namespace-level:** Apply `AuthorizationPolicy` at namespace scope for coarse allow/deny. Use for broad segmentation (e.g., allow all from `team-a` namespace to `api` namespace).

**Workload-level:** Attach policies to specific workloads for fine-grained control. Use `selector` to target pods by labels. Prefer workload-level when namespace boundaries are insufficient.

**Deny-by-default:** Explicitly deny all traffic, then allow only required paths. Reduces blast radius of misconfigurations. Document every allow rule with a business justification.

## Common Pitfalls

- **Mesh-wide strict mTLS breaking non-mesh services:** External callers, legacy workloads, or ingress paths that cannot present mesh certs will fail. Use permissive mode for those paths or exclude them from the mesh until they support mTLS.

- **Sidecar resource overhead ignored:** Unbounded proxy resources can cause node pressure and evictions. Set requests/limits and monitor utilization.

- **Policy conflicts:** Overlapping `AuthorizationPolicy` and `PeerAuthentication` rules can produce unexpected denials. Audit policies for conflicts; use a single source of truth per namespace where possible.

- **Observability gaps in mesh-to-mesh communication:** Multi-cluster or multi-mesh scenarios often lack unified tracing and metrics. Ensure trace context propagation and consistent metric labels across mesh boundaries.

## Decision Framework for Mesh Selection

1. **Policy needs:** Require per-pod L7 policy? Prefer sidecar. Need only network-level segmentation? Consider Cilium or ambient.
2. **Operational maturity:** New to meshes? Start with a single-mesh, single-cluster deployment. Scale to multi-cluster only after SRE familiarity.
3. **Platform fit:** Align with existing orchestrator (Kubernetes), ingress, and observability stack. Avoid mesh sprawl across multiple incompatible implementations.
4. **Performance budget:** If latency or resource overhead is constrained, favor ambient or lightweight proxies.

## Workflow

1. Map service communication paths and trust boundaries.
2. Define mesh policies for mTLS, authorization, retries, and timeouts.
3. Configure traffic policies for rollout and fault isolation.
4. Validate telemetry, health behavior, and failure recovery.
5. Produce remediation and hardening recommendations.

## Output Format

```markdown
## Mesh Architecture Summary
- Scope: <services/namespaces>
- Trust model: <mTLS/authz approach>
- Mode: <sidecar | ambient | hybrid>
- Control plane: <replicas, HA strategy>

## Policy Plan
- Security policies: <list with rollout strategy: permissive -> strict>
- Traffic policies: <list>
- Authorization: <namespace/workload-level, deny-by-default?>

## Data Plane Overhead
- Baseline vs post-mesh: <CPU/memory delta>
- Per-pod proxy resources: <requests/limits>

## Validation Checklist
- [ ] mTLS and authz policies enforced
- [ ] Routing behavior matches intent
- [ ] Retry/timeout settings validated
- [ ] Non-mesh callers excluded or permissive paths defined
- [ ] Certificate rotation tested

## Common Pitfalls Addressed
- <pitfall> -> <mitigation applied>

## Risks and Mitigations
- <risk> -> <mitigation>

## Mesh Selection Rationale
- <decision> -> <reason>
```

## Constraints

- Prefer gradual policy rollout to avoid broad outages.
- Keep policy intent explicit and auditable.
- Validate both happy path and failure path behavior.
