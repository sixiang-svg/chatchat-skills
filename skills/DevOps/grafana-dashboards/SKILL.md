---
id: grafana-dashboards
name: Grafana Dashboards
description: Design Grafana dashboards that are actionable, low-noise, and aligned to service objectives. Use when building new dashboards or improving observability for incidents, SLOs, and on-call workflows.
category: DevOps
requires: []
examples:
  - Build a service health dashboard with latency, error rate, and saturation panels by environment.
  - Refactor a noisy dashboard into a focused incident view with drill-down links and annotations.
---

# Grafana Dashboards

Design dashboards that help operators decide what to do next, not just display charts.

## When to Use

- You need a clear service health view for on-call or incident response.
- You are introducing or refining SLI/SLO-aligned visualizations.
- You want to reduce alert triage time with better panel design.

## Panel Design Patterns

**USE method (Utilization, Saturation, Errors):** For resources (CPU, memory, disk). Use gauges for utilization %, stat panels for saturation (queue depth, connection count), and counters for errors. Best for infrastructure and capacity views.

**RED method (Rate, Errors, Duration):** For request-driven services. Rate = requests/sec (graph). Errors = error rate % or count (stat or graph). Duration = latency percentiles (graph with p50, p95, p99). Best for APIs and microservices.

**Stat vs gauge vs graph:** Use stat for single-value status (current error rate, SLO burn). Use gauge for bounded metrics (utilization 0-100%). Use graph for time-series trends (latency over time, traffic patterns). Avoid graphs for values that rarely change.

## PromQL Query Patterns

**Error rate:**
```promql
sum(rate(http_requests_total{status=~"5.."}[5m])) by (service) / sum(rate(http_requests_total[5m])) by (service) * 100
```

**Latency percentiles (p50, p95, p99):**
```promql
histogram_quantile(0.50, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))
histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, service))
```

**Saturation (queue depth, connections):**
```promql
avg(queue_depth) by (service)
sum(active_connections) by (instance)
```

Use `$__rate_interval` or `5m` for rate queries; align with scrape interval. Add `by (service, env)` when variables exist.

## Variables and Annotations

**Variables:** Add `service`, `env`, `region` as dropdowns. Use `label_values(metric, label)` for dynamic options. Set sensible defaults (e.g. `All` or most common env). Avoid more than 4-5 variables; each adds cognitive load.

**Annotations:** Add deploy annotations (from CI/CD or release pipeline) and incident annotations (from PagerDuty, Opsgenie). Use distinct colors for deploys vs incidents. Annotations reduce "what changed?" guesswork during triage.

## Common Pitfalls

- **Too many panels:** Dashboards with 20+ panels overwhelm. Limit to 8-12 high-signal panels; use links to drill-down dashboards for deep dives.
- **Unclear units:** Label axes (e.g. "ms", "req/s", "%"). Use `legendFormat` to clarify series.
- **Missing thresholds:** Set threshold bands on gauges/stats (green/yellow/red) so status is visible at a glance.
- **No drill-down links:** Add links from panels to logs (Loki), traces (Tempo/Jaeger), or runbooks. Use template variables in URLs.
- **Stale dashboards:** Dashboards that no one updates become useless. Assign ownership; review quarterly.

## Dashboard-as-Code

**JSON provisioning:** Store dashboard JSON in version control. Use Grafana provisioning (configmap, file) to load dashboards. Enables review, rollback, and consistency across environments.

**Grafonnet:** Use Jsonnet (grafonnet library) to generate dashboards from reusable components. Reduces duplication; parameterize service names, datasources, and panels. Suits multi-service or multi-tenant setups.

## Workflow

1. Define audience and decisions the dashboard must support.
2. Choose core signals: latency, traffic, errors, saturation; dependency health where relevant.
3. Apply USE or RED patterns; select stat/gauge/graph per panel.
4. Organize top-down: status summary, diagnostics, deep dives.
5. Add variables (service, env) and annotations (deploys, incidents).
6. Add drill-down links to logs, traces, runbooks.
7. Validate units, labels, thresholds; verify default time range supports triage.

## Panel Quality Checklist

- [ ] Titles are specific and action-oriented.
- [ ] Units and legend names are unambiguous.
- [ ] Time ranges and resolution match signal volatility.
- [ ] Color semantics are consistent (warning/critical).
- [ ] Thresholds set on gauges/stats.
- [ ] Drill-down links present where useful.

## Output Format

```markdown
## Dashboard Intent
- Audience: <on-call, SRE, dev>
- Primary decisions: <what operators must decide>

## Panel Map
| Panel | Type | Purpose | PromQL/Query | Thresholds |
|-------|------|---------|--------------|------------|
| ...   | stat | ...     | ...          | ...        |

## Variables
- service: <source, default>
- env: <source, default>

## Annotations
- Deploys: <source>
- Incidents: <source>

## Drill-Down Links
- Error panel -> Loki: <URL pattern>
- Latency panel -> Tempo: <URL pattern>

## Gaps and Next Steps
- Missing: <panels or alerts>
- Risks: <stale data, unclear ownership>
- Recommended: <next panel or alert improvements>
```

## Constraints

- Avoid dashboards with duplicate panels and unclear ownership.
- Keep default view focused on high-signal service state.
- Do not claim SLO compliance without explicit SLI definition.
- Keep alert thresholds versioned and tied to owner-reviewed expectations.