---
id: export
name: Export
description: Implement reliable data export workflows with correct formatting, filtering, access control, and large-volume handling.
category: Development
requires: ["source data schema", "export format (csv/json/xlsx/pdf)", "filter and permission rules"]
examples:
  - "Design an export endpoint for transaction history as CSV with date filters and role-based access."
  - "Implement batch export for large datasets with async job processing and download links."
---

# Export

Create export features that are correct, secure, and scalable for real user data volumes.

## When to Use

- You need to build or improve data export functionality.
- Exports must handle large datasets and user permissions safely.

## Workflow

1. Define export fields, filters, and format requirements.
2. Enforce authorization and data-scope restrictions.
3. Choose sync vs async export based on expected volume.
4. Add retries, progress tracking, and file lifecycle policies.
5. Validate correctness with sample and edge-case datasets.

## Output

- Export architecture and API plan
- Security and scalability notes
- Validation and operations checklist
