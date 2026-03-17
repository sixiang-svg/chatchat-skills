---
id: agentdb-vector-search
name: AgentDB Vector Search
description: AgentDB memory system with HNSW vector search for pattern storage and semantic lookup.
category: Research
requires: []
examples:
  - Store this coding pattern in my long-term memory for future use.
  - Search my memory for previous solutions to Python memory errors.
---
# Memory Management Skill

## Purpose
Guide the agent to manage a persistent memory system for pattern storage and semantic lookup using vector search principles.

## When to Trigger
- When the user identifies a successful solution or coding pattern that should be reused.
- When the user asks to recall previous experiences, solutions, or specific data points.
- When semantic lookup is required to solve a current problem based on historical context.

## When to Skip
- For ephemeral or one-time tasks that do not provide long-term learning value.
- When the user explicitly requests not to store information.

## Behavioral Instructions
1. **Semantic Retrieval**: When a search is required, use the `rag_data_search` tool to perform a semantic lookup. Formulate queries that focus on the core intent and technical keywords of the user's request.
2. **Information Synthesis**: After retrieving data from memory, prioritize accuracy and explain how the past solution applies to the current context.
3. **Pattern Identification**: Proactively suggest storing information if you identify a complex, multi-step solution that the user might need in the future.
4. **Formatting**: Present retrieved memory results clearly. Use bold text for key patterns and code blocks for technical solutions.

## Best Practices
1. Check existing memory using `rag_data_search` for relevant patterns before proposing a new solution.
2. When the user confirms a solution works, summarize it into a concise "Knowledge Nugget" for future storage.
3. Use hierarchical organization when discussing complex system architectures.
4. Always document any new learnings or edge cases found during the current session.