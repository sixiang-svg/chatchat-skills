---
id: prometheus-configuration
name: Prometheus Configuration
description: Configure Prometheus scraping, recording rules, and alerting to produce actionable service reliability signals.
category: DevOps
requires: []
examples:
  - Help configure Prometheus metrics and alerts for this service.
  - Review our Prometheus setup for noisy alerts and missing coverage.
---

# Prometheus Configuration

Set up Prometheus in a way that supports fast detection and triage.

## When to Use

- You are defining metrics, scraping, or alert rules.
- You need better reliability visibility and lower alert noise.
- You want SLO-aligned monitoring coverage.

## Scrape Configuration Patterns

**Static targets** for fixed endpoints:

```yaml
scrape_configs:
  - job_name: 'api'
    static_configs:
      - targets: ['api-1:9090', 'api-2:9090']
        labels:
          env: prod
          team: backend
```

**Kubernetes service discovery** for dynamic targets:

```yaml
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
        action: replace
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: ${1}:${2}
        target_label: __address__
      - action: labelmap
        regex: __meta_kubernetes_pod_label_(.+)
```

Use relabeling to drop high-cardinality labels, rename targets, or filter scrapes. Avoid labels like `user_id`, `request_id`, or unbounded path segments.

## Recording Rules

Precompute expensive aggregations to speed dashboards and alerts:

```yaml
groups:
  - name: api_aggregates
    interval: 1m
    rules:
      - record: job:http_requests:rate5m
        expr: sum(rate(http_requests_total[5m])) by (job, status)
      - record: job:http_request_duration_seconds:histogram_quantile_p99
        expr: histogram_quantile(0.99, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, job))
```

Do not duplicate raw metrics; record only aggregates. Keep `interval` aligned with scrape interval (e.g., 2-4x scrape interval).

## Alert Rule Design

Use `for` to reduce flapping, and include labels and annotations for triage:

```yaml
groups:
  - name: api_alerts
    rules:
      - alert: HighErrorRate
        expr: job:http_requests:rate5m{status=~"5.."} / job:http_requests:rate5m > 0.05
        for: 5m
        labels:
          severity: critical
          team: backend
        annotations:
          summary: "High error rate on {{ $labels.job }}"
          description: "Error rate {{ $value | humanizePercentage }} exceeds 5% for 5 minutes."
          runbook_url: "https://runbooks.example.com/high-error-rate"
```

Always set `for` (e.g., 2-5 minutes) for rate-based alerts. Include `runbook_url` for on-call handoff.

## Common Pitfalls

- **High-cardinality labels**: Labels like `user_id`, `path` with many values bloat TSDB and slow queries. Use relabeling to drop or aggregate.
- **Missing relabeling**: K8s discovery yields many meta-labels; use `relabel_configs` to keep only what you need.
- **Scrape interval too aggressive**: Sub-15s intervals increase load; 15-30s is typical for most targets.
- **Alerts without `for`**: Instant spikes cause alert storms; add `for: 2m` or more.
- **Recording rules duplicating raw metrics**: Record only aggregates; avoid `record: http_requests_total` or similar.

## Workflow

1. Identify critical services and target metrics.
2. Define scrape targets and label strategy.
3. Create recording rules for key aggregates.
4. Define alert rules tied to user-impact thresholds.
5. Validate signal quality and tune alert noise.

## Output Format

```markdown
## Scrape Plan
- Job name: <name>
- Discovery: static_configs | kubernetes_sd_configs | <other>
- Targets: <list or discovery role>
- Interval: <value, e.g. 15s>
- Relabeling: <key actions; drop high-cardinality labels, add env/team>

## Recording Rules
- Rule name: <record name>
  - Expr: <PromQL>
  - Interval: <value>

## Alert Rules
- Alert: <name>
  - Expr: <PromQL>
  - For: <duration>
  - Labels: severity, team
  - Annotations: summary, description, runbook_url

## Validation
- [ ] Metrics present and labeled correctly
- [ ] No high-cardinality labels on hot metrics
- [ ] Recording rules use aggregates, not raw duplication
- [ ] Alerts have `for` clause and runbook_url
- [ ] Scrape interval appropriate for target load
- [ ] Alerts trigger correctly in test
- [ ] Noise level acceptable
```
