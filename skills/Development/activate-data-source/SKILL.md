---
id: activate-data-source
name: Activate Data Source
description: Safely activate a new data source by validating connectivity, schema mapping, permissions, and ingestion readiness before enabling it in production.
category: Development
requires: ["data source connection string", "access credentials"]
examples:
  - "Activate this Postgres data source for staging and verify schema mapping before enabling ingestion."
  - "Enable this API data source and run a preflight check for auth, field mapping, and rate limits."
---

# Activate Data Source

Use this skill when onboarding or enabling a new data source in an application, ETL pipeline, or analytics platform.

## When to Use

- A new source (database/API/file feed) must be connected and enabled.
- You need to validate credentials, schema alignment, and access scope before activation.
- You want a repeatable preflight checklist to reduce runtime failures.

## Workflow

1. Identify source type, environment (dev/staging/prod), and owner.
2. Validate authentication and least-privilege access.
3. Test network connectivity and query/read permissions.
4. Compare source schema to expected contract (types, nullability, keys).
5. Define mapping and transformations (field names, timezones, enums).
6. Run a limited ingestion dry-run and inspect errors.
7. Set monitoring (error rate, lag, throughput) and alert thresholds.
8. Activate behind a flag or staged rollout when possible.

## Common Checks

- Credentials and token expiry policy
- Rate limits and retry strategy
- PII/sensitive field handling and masking
- Idempotency and duplicate prevention
- Backfill strategy and replay behavior

## Output

- Activation checklist with pass/fail status
- Risks and blockers, with recommended fixes
- Go/no-go recommendation and rollout plan
