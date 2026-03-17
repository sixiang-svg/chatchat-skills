---
id: add-dataset
name: Add Dataset
description: Add a new dataset with schema validation, quality checks, metadata registration, and ingestion readiness.
category: Development
requires: [".csv"]
examples:
  - "Add this CSV dataset and validate schema, null rates, and primary keys before ingestion."
  - "Prepare this dataset for production use with metadata, lineage notes, and quality checks."
---

# Add Dataset

Use this skill when introducing a new dataset into an app, pipeline, or model workflow.

## When to Use

- A new file/table/feed must be onboarded.
- You need to verify schema, data quality, and compatibility.
- You want traceability (ownership, lineage, update cadence).

## Workflow

1. Identify dataset source, format, owner, and refresh schedule.
2. Profile structure (columns/types/row counts/cardinality).
3. Validate constraints (required fields, unique keys, value ranges).
4. Check quality metrics (null %, duplicates, outliers, drift).
5. Define target schema mapping and transformations.
6. Register metadata (owner, lineage, retention, sensitivity).
7. Run a sample load and verify downstream compatibility.
8. Approve ingestion with monitoring and alerts.

## Common Pitfalls

- No stable primary key
- Mixed timestamp formats/timezones
- Silent type coercion in ETL
- Missing data sensitivity classification
- No incremental load strategy

## Output

- Dataset onboarding checklist
- Data quality report summary
- Ingestion go/no-go recommendation
