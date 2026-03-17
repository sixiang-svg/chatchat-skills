---
id: benchling-integration
name: Benchling Integration
description: Guidance for using Benchling Python SDK and REST API to manage biological entities, inventory, and workflows.
category: Research
requires: []
examples:
  - How do I authenticate with the Benchling Python SDK using an API key?
  - What are the steps to create and register a new DNA sequence in the Benchling Registry?
  - Explain how to automate a container transfer in Benchling Inventory.
  - How can I link an experimental result to a specific notebook entry via the API?
---

## Instruction
- Initialize the Benchling SDK by selecting the appropriate authentication method: use API Key authentication for simple automation scripts or OAuth2 Client Credentials for long-lived applications and Benchling Apps.
- Define the biological entity to be managed, such as DNA sequences, RNA, or proteins, ensuring all required metadata and schema fields are identified.
- Manage the Registry by creating new entities, updating existing records, or archiving obsolete entries. Use specific registration strategies to ensure unique IDs are generated correctly.
- Orchestrate inventory operations by programmatically creating containers, plates, or boxes, and executing transfers between storage locations.
- Document experimental data in the Electronic Lab Notebook (ELN) by creating or updating entries, managing templates, and linking entities or results directly to notebook records.
- Automate laboratory processes through the Workflow system by creating tasks, assigning them to users, and monitoring status changes asynchronously.
- Implement event-driven integrations by configuring Benchling to route events (like entity creation or workflow updates) to AWS EventBridge for downstream processing.
- Perform high-level analytics by querying the Benchling Data Warehouse via SQL to aggregate experimental results or monitor inventory trends.
- Apply best practices for API usage, including implementing retry strategies for rate limits, using generators for memory-efficient pagination, and ensuring all credentials are stored in secure environment variables.

## When to Use
- When programmatically managing biological sequences and metadata within the Benchling cloud platform.
- When automating high-throughput laboratory operations such as sample tracking, inventory transfers, and plate mapping.
- When building custom Benchling Apps or syncing data between Benchling and external laboratory information systems.
- When generating automated reports or conducting data science workflows using Benchling-resident experimental data.

## Output
- A logical roadmap for implementing Benchling-based automations using the Python SDK or REST API.
- Summarized steps for data modeling, entity registration, and workflow task management.
- Technical advice on security, error handling, and performance optimization for life science data integrations.