---
id: agent-evaluation
name: Agent Evaluation
description: Guidance for implementing self-critique, reflection loops, and evaluator-optimizer pipelines.
category: Research
requires: []
examples:
  - How do I implement a reflection loop for my coding agent?
  - Create a rubric-based evaluation system for agent generated reports.
---
# Agentic Evaluation Instructions

## Purpose
Guide the agent to perform iterative self-improvement through reflection loops, critique, and optimization patterns.

## Behavioral Logic: Generate → Evaluate → Critique → Refine
When this skill is activated, you must move beyond single-shot generation and follow this iterative cycle:

1. **Initial Generation**: Produce the initial response based on the user's task.
2. **Critique**: Evaluate the generated output against provided criteria or standard quality metrics (accuracy, clarity, completeness). 
3. **Refine**: If the evaluation does not meet the "PASS" threshold, identify specific "FAIL" areas and rewrite the content to address those failures.

## Evaluation Patterns to Apply

### 1. Basic Reflection Pattern
- Review your own response.
- Identify at least two potential weaknesses or edge cases.
- Provide a refined version that addresses these points.

### 2. Evaluator-Optimizer Pattern
- Act as a separate "Evaluator" component. 
- Assign a score (0.0 to 1.0) based on the user's requirements.
- Only output the final result once a threshold of 0.8 is achieved or max iterations (default: 3) are reached.

### 3. Rubric-Based Assessment
When generating complex reports or code:
- Create a multi-dimensional rubric (e.g., Accuracy, Readability, Security).
- Rate each dimension from 1-5.
- Explicitly state the reasoning for each score before providing the final improved output.

## Constraints and Best Practices
- **Iteration Limits**: Do not exceed 3-5 iterations to prevent infinite loops.
- **Structured Critique**: Always format internal critiques clearly (using JSON structure if necessary for internal logic) to ensure all requirements are addressed.
- **Convergence**: If the quality does not improve between two consecutive iterations, stop and provide the best available version with a note on limitations.
- **Code-Specific Reflection**: For coding tasks, mentally simulate the execution or generate test cases to verify the logic before finalizing the response.

## Quick Start Checklist for Execution
- [ ] Define specific evaluation criteria before starting the refinement loop.
- [ ] Perform a "Self-Critique" step for every high-stakes response.
- [ ] Verify that the final output addresses all "FAIL" points identified during the reflection stage.