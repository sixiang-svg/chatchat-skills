---
id: loki-mode
name: Loki Mode
description: Investigate logs in Grafana Loki with fast, repeatable queries and issue-focused triage steps. Use when debugging production incidents, validating deployments, or tracing request failures.
category: DevOps
requires: []
examples:
  - Investigate 500 errors in the last 30 minutes using Loki labels for service and environment.
  - Build a focused Loki query to compare error volume before and after a deployment.
---

# Loki Mode

Investigate incidents in Grafana Loki with a repeatable LogQL workflow that narrows scope fast and produces evidence-backed conclusions.

## When to Use

- You are diagnosing production errors, latency spikes, or failed jobs from centralized logs.
- You need high-signal LogQL queries instead of broad text searching.
- You need a timestamped evidence trail for incident handoff.

## Workflow

1. Set scope first: `service`, `environment`, `region`, time range, and expected baseline.
2. Start with label filters, then add content filters:
   - Labels first: `app`, `namespace`, `cluster`, `level`
   - Then line filters: `|= "timeout"` or `|~ "pattern"`
3. Build from broad to narrow:
   - Count error volume
   - Break down by endpoint/job
   - Inspect representative lines
4. Compare "before deploy" vs "after deploy" windows to validate regression.
5. Correlate with Grafana dashboard annotations: add deployment markers and link queries to the same time range for visual correlation.
6. Extract `traceID` from JSON logs and link to the tracing backend for end-to-end request inspection.
7. Save the final query and include key timestamps for responders.

## LogQL Techniques

**line_format:** Restructure output for readability. Example: `{app="api"} | json | line_format "{{.timestamp}} {{.level}} {{.msg}} path={{.path}}"` to focus on specific fields.

**unwrap:** Derive metrics from log fields. Example: `{app="api"} | json | unwrap duration_ms | __error__="" | sum by (path)` to aggregate latency by endpoint. Use `__error__=""` to drop parse failures.

**Pattern matching:** Use `|~ "regex"` for flexible matching; anchor with `^` and `$` when needed. Prefer `|= "literal"` when possible; it is faster and avoids regex cost.

**Multi-line logs:** Use `| regexp "(?P<msg>.*)"` or `| pattern` to parse stack traces. For JSON logs spanning lines, ensure your log pipeline emits single-line JSON or use `| json` with `line_format` to join continuation lines if supported.

## Query Patterns

- Error stream by service: `{app="api", env="prod", level=~"error|fatal"}`
- Endpoint-specific failures: `{app="api", env="prod"} |= "/checkout" |= "500"`
- JSON logs by error type: `{app="worker", env="prod"} | json | level="error" | stats count() by err_code`
- Deployment comparison: `{app="api", env="prod"} | json | stats count() by status`
- Latency percentiles from logs: `{app="api"} | json | unwrap duration_ms | quantile_over_time(0.99, 1m) by (path)`
- Restructured output: `{app="api"} | json | line_format "{{.timestamp}} {{.level}} {{.path}} {{.request_id}}"`

## Common Pitfalls

- **Querying without label filters:** Omitting stream selectors causes full scans across all streams. Always start with `{app="...", env="..."}` or equivalent.
- **Overly broad regex:** `|~ ".*error.*"` matches too much and is slow. Prefer `|= "error"` or targeted regex like `|~ "timeout|deadline"`.
- **Ignoring log volume for cost:** Wide time ranges and unbounded queries increase read volume and cost. Tighten time range and labels first.
- **Not using stream selectors first:** Content filters alone scan everything. Labels reduce the working set before line filters run.

## Output Format

Return:

- Incident scope (`service`, `env`, user impact estimate)
- Final LogQL queries used (with stream selectors shown)
- Evidence summary (timestamps, signatures, trend direction)
- Correlation links: Grafana dashboard annotation timestamps, traceID extraction query if applicable
- Most likely root-cause hypothesis and one verification action

## Constraints

- Keep time ranges tight; expand only when needed.
- Prefer structured label filtering over free-text matching.
- Do not assert root cause without at least two corroborating signals (pattern + timing or pattern + metric).
