---
id: python-observability
name: Python Observability
description: Implement Python observability with structured logs, metrics, and traces to speed up incident detection and root-cause analysis.
category: DevOps
requires: []
examples:
  - Design observability instrumentation for a Python API service in production.
  - Improve signal quality by reducing noisy logs and adding actionable metrics.
---

# Python Observability

Establish practical observability for Python services and background workers.

## When to Use

- You need better visibility into Python service health and performance.
- You are diagnosing incidents with limited logs or missing traces.
- You need consistent telemetry conventions across environments.

## Workflow

1. Define service-level objectives and key user-facing signals.
2. Specify structured logging fields and correlation identifiers.
3. Add metrics for latency, throughput, errors, and resource usage.
4. Instrument traces at critical request and dependency boundaries.
5. Validate dashboards and alerts against realistic failure scenarios.

## Library Patterns

**Structured logging:** Use `structlog` or `python-json-logger` for JSON output. Structlog example: `structlog.configure(processors=[structlog.processors.JSONRenderer()])` and `logger.info("request_completed", path=path, status=status, duration_ms=duration)`. Avoid `print()` in production; it bypasses levels and produces unstructured output.

**Metrics:** Use `prometheus_client` for counters, histograms, and gauges. Example: `REQUEST_LATENCY = Histogram("http_request_duration_seconds", "Request latency", ["method", "path"])` with low-cardinality labels. Export via `/metrics` endpoint; never block the main thread on push or scrape.

**Traces:** Use `opentelemetry-sdk` with `opentelemetry-instrumentation-fastapi`, `opentelemetry-instrumentation-django`, or `opentelemetry-instrumentation-flask` for auto-instrumentation. Add manual spans at business boundaries: `with tracer.start_as_current_span("process_order") as span: span.set_attribute("order_id", order_id)`.

## Middleware Integration

**FastAPI:** Add `opentelemetry.instrumentation.fastapi.FastAPIInstrumentor().instrument_app(app)` before `app.run()`. For structlog, use middleware that injects `request_id` and `trace_id` into the context and logs them on every request.

**Django:** Use `opentelemetry.instrumentation.django.DjangoInstrumentor().instrument()` in `settings.py`. Add a custom middleware that sets `request_id` from headers or generates one, and passes it to `structlog.contextvars.bind()`.

**Flask:** Apply `opentelemetry.instrumentation.flask.FlaskInstrumentor().instrument_app(app)`. Use `before_request` to bind `request_id` and `trace_id` to the logging context so all logs in the request scope include them.

## Common Pitfalls

- **Print-based logging in production:** Prints are unstructured, lack levels, and cannot be filtered. Replace with structured loggers.
- **Unstructured log formats:** Free-form strings prevent aggregation and alerting. Use JSON with fixed keys.
- **Missing request_id propagation:** Without correlation IDs across services, tracing a request through the stack is impossible. Propagate `X-Request-ID` or W3C traceparent headers.
- **Blocking metric exports:** Pushing metrics synchronously blocks the event loop. Use async exporters or expose a scrape endpoint.
- **Ignoring GIL impact on trace timing:** CPU-bound spans under GIL can show inflated durations. Use `opentelemetry-instrumentation` with care for CPU-heavy code; consider process-based parallelism for accurate timing.

## Concrete Code Patterns

**Logging:** `logger.info("payment_processed", order_id=order_id, amount=amount, currency=currency, request_id=request_id)`; always include correlation IDs.

**Metrics:** `ERROR_COUNTER.labels(method="POST", path="/checkout").inc()` on error paths; `REQUEST_LATENCY.labels(method=method, path=path).observe(duration)` on completion.

**Traces:** Wrap external calls: `with tracer.start_as_current_span("db_query") as span: span.set_attribute("db.statement", sanitized_query); result = conn.execute(query)`.

## Output Format

```markdown
## Telemetry Plan
- Service: <name>
- Signals: <logs/metrics/traces>
- SLOs: <availability/latency targets>
- Libraries: structlog/python-json-logger, prometheus_client, opentelemetry-sdk

## Instrumentation Map
- Entry points: <api/jobs/consumers>
- Dependencies: <db/cache/external api>
- Correlation fields: <trace_id/request_id/user_id>
- Middleware: <framework-specific instrumentation and request_id binding>

## Code Patterns
- Logging: <structured log call example with correlation IDs>
- Metrics: <counter/histogram usage for key paths>
- Traces: <span boundaries for critical operations>

## Readiness Checklist
- [ ] Error budget metrics available
- [ ] Trace coverage on critical paths
- [ ] Alert thresholds mapped to SLOs
- [ ] request_id propagated across service boundaries
- [ ] No print() or unstructured logs in production paths
```

## Constraints

- Prefer low-cardinality metric labels for stable dashboards.
- Do not include sensitive data in logs, spans, or metric labels.
- Keep recommendations framework-agnostic unless requested.
