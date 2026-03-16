---
id: monitor-experiment
name: Monitor Experiment
description: Monitor Beaker experiments until completion, checking status and retrieving failure logs.
category: Research
requires: []
examples:
  - Monitor Beaker experiment 01KCW39T and notify me when it finishes.
  - Get the logs for my failed experiment and explain the exit code.
---

# Monitor Beaker Experiment

## Instructions

When monitoring a Beaker experiment:

1. Get the experiment status using `beaker experiment get <experiment-id>`
2. Check if the experiment has completed by looking at `status.exited`
3. If still running, wait 30 seconds and check again
4. When complete:
   - If exitCode is 0: Report success
   - If exitCode is non-zero: Fetch and display logs with `beaker experiment logs <experiment-id>`
5. Continue monitoring until the experiment finishes or the user asks you to stop

## When to Use
- When managing long-running computational experiments or model training sessions on the Beaker platform.
- When needing automated notifications or summaries of experiment success and failure.
- When debugging failed remote jobs by programmatically retrieving logs and exit codes.

## Output
- Real-time status updates and a final experiment summary (Success/Failure/Exit Code).
- Extracted error logs and diagnostic explanations for failed experiments.
- Actionable next steps for re-submitting or adjusting the experiment parameters.