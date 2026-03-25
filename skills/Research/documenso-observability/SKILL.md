---
id: documenso-observability
name: Documenso Observability
description: Implement monitoring, logging, and tracing for Documenso integrations to debug production issues and collect metrics.
category: Research
author: Jeremy Longshore <jeremy@intentsolutions.io>
version: 1.0.0
requires: []
examples:
  - Help me set up Prometheus metrics for my Documenso integration.
  - Configure structured logging for debugging Documenso API requests.
---

# Documenso Observability

## Overview
Implement comprehensive observability for Documenso integrations including metrics, logging, and distributed tracing.

## Prerequisites
- Working Documenso integration
- Monitoring platform (Datadog, Prometheus, etc.)
- Logging infrastructure (ELK, CloudWatch, etc.)
- Tracing system (Jaeger, Zipkin, etc.)

## Instruction
- Define core Prometheus metrics including counters for requests/errors, histograms for latency, and gauges for active documents.
- Implement an instrumented client wrapper using a Proxy to automatically track API operation performance and status.
- Set up a dedicated `/metrics` endpoint to expose collected data for Prometheus scraping.
- Configure a structured logger with Pino, ensuring sensitive information (API keys, tokens, signatures) is redacted before logging.
- Implement specialized logging for API requests and webhook events, including metadata like duration and processing success.
- Initialize OpenTelemetry SDK to enable distributed tracing with OTLP exporters and automated instrumentations.
- Wrap critical Documenso operations with custom spans to provide detailed trace visibility into the signing workflow.
- Create a health check endpoint that validates Documenso connectivity and reports latency and service status.
- Define Prometheus alerting rules to detect high error rates, excessive latency, or service downtime.

## When to Use
- When implementing monitoring, logging, and tracing for Documenso integrations to debug production issues.
- When setting up performance metrics and health monitoring for digital signature workflows.
- When requiring distributed tracing to understand the lifecycle of document creation and signing events.

## Output
- Prometheus metrics exposed
- Structured logging configured
- Distributed tracing enabled
- Health checks implemented
- Alerting rules defined

## Error Handling
| Observability Issue | Cause | Solution |
|--------------------|-------|----------|
| Metrics not showing | Wrong scrape config | Check Prometheus config |
| Logs not appearing | Log level too high | Set LOG_LEVEL=debug |
| Traces missing | OTEL not initialized | Call initTracing() |
| High cardinality | Too many labels | Reduce label values |

