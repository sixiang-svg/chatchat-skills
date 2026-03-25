---
id: safety-system-skill
name: Safety System Skill
description: System safety skill that prevents agent deadlocks via non-LLM control commands to inspect task state and flush message queues.
category: Research
requires: []
examples:
  - Help me recover the system from a deadlock using control commands.
  - How do I inspect the current task registry state and system health?
---

# error-guard

⚠️ **System‑level skill (Advanced users)**

This skill defines the **control‑plane safety primitives** for OpenClaw.
It is intentionally minimal, non‑blocking, and designed to prevent agent freezes, deadlocks, and unrecoverable states when running long‑lived or high‑risk workloads.

## Design Principles

> **Warning:** This skill operates at the agent control‑plane level.
> It should be installed only by users who understand OpenClaw’s execution model and are running workloads that can block, hang, or run for extended periods.

- **Main agent never blocks**: no long exec, no external I/O, no LLM calls.
- **Event-driven**: workers emit events; the control plane listens.
- **Fail-safe first**: recovery commands must always respond.
- **Minimal state**: track only task metadata (never payloads).

## Command Surface (Phase 1)

### /status

Report current system health and task registry state.

Returns:
- Active tasks (taskId, type, state)
- Start time and last heartbeat
- Flags for stalled or overdue tasks

Constraints:
- Must run in constant time
- Must not call any model or external API

### /flush

Emergency stop.

Immediately:
- Cancel all active tasks
- Kill active exec/process sessions
- Clear pending message queue
- Reset in-memory task registry

Constraints:
- Must always respond
- No waiting on workers
- No model calls

### /recover

Safe recovery sequence.

Steps:
1. Execute `/flush`
2. Reset control-plane state
3. Optionally reload skills/state (no container restart)

## Future Extensions (Not Implemented Yet)

- Sub-agent runner helper (event-driven)
- Task watchdogs with TTL and silence detection
- Structured event protocol (task.started, task.heartbeat, task.completed, ...)
- Back-pressure and task classes (interactive / batch / background)

## Security & Privacy

- This skill **does not** store payloads, prompts, messages, or model outputs
- Only minimal task metadata is persisted (taskId, timestamps, state)
- No API keys, credentials, or user data are read or written
- Safe to publish and share publicly

## Non-Goals

- No business logic
- No background polling loops
- No user-facing features
- No LLM reasoning paths

This skill is the **last line of defense**. Keep it small, fast, and reliable.

## Instruction
- Utilize non-LLM control commands to inspect the agent's internal task registry and system health without blocking execution.
- Run `/status` periodically to identify stalled or overdue tasks and report the current heartbeat of the control plane.
- Execute the `/flush` command as an emergency stop to immediately cancel all active tasks and clear pending message queues.
- Perform the `/recover` sequence to reset the agent's state and reload necessary skills after a system freeze or deadlock.
- Strictly adhere to constant-time constraints for safety commands, ensuring they never call external APIs or LLM models.
- Monitor minimal task metadata (ID, timestamps) to maintain a fail-safe environment for long-lived or high-risk workloads.

## When to Use
- When running high-risk, long-duration tasks that are prone to agent freezes or infinite loops.
- When requiring an emergency "kill switch" to stop active code execution or message processing.
- When performing automated system health monitoring for complex multi-agent orchestration.

## Output
- Real-time system health reports including task IDs and start times.
- Detailed recovery logs summarizing the outcome of flush and reset operations.
- Actionable status flags for stalled processes and suggested recovery paths.