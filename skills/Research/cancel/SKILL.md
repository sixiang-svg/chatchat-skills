---
id: cancel
name: Cancel
description: Cancel any active OMC mode (autopilot, ralph, swarm, etc.) and perform state cleanup.
category: Research
requires: []
examples:
  - Cancel the current autopilot workflow and preserve progress.
  - Force clear all active sessions and reset the workspace.
---

# Cancel Skill

Intelligent cancellation that detects and cancels the active OMC mode.

**The cancel skill is the standard way to complete and exit any OMC mode.**
When the stop hook detects work is complete, it instructs the LLM to invoke
this skill for proper state cleanup. If cancel fails or is interrupted,
retry with `--force` flag, or wait for the 2-hour staleness timeout as
a last resort.

## What It Does

Automatically detects which mode is active and cancels it:
- **Autopilot**: Stops workflow, preserves progress for resume
- **Ralph**: Stops persistence loop, clears linked ultrawork if applicable
- **Ultrawork**: Stops parallel execution (standalone or linked)
- **UltraQA**: Stops QA cycling workflow
- **Swarm**: Stops coordinated agent swarm, releases claimed tasks
- **Ultrapilot**: Stops parallel autopilot workers
- **Pipeline**: Stops sequential agent pipeline
- **Team**: Sends shutdown_request to all teammates, waits for responses, calls TeamDelete, clears linked ralph if present
- **Team+Ralph (linked)**: Cancels team first (graceful shutdown), then clears ralph state. Cancelling ralph when linked also cancels team first.

## Instruction
You are the System State and Cleanup Coordinator. When this skill is activated, you must guide the agent through an intelligent cancellation protocol for active OMC (Oh-My-ClaudeCode) modes using the following behavioral logic:

1. **Session-Aware Detection**: Instruct the system to inspect the current session state via the state registry to identify active modes such as Autopilot, Ralph, Swarm, or Team. 
2. **Dependency-Ordered Shutdown**: Ensure cancellation follows a strict hierarchy to prevent orphaned processes:
   - **Phase 1 (Workflows)**: Cancel Autopilot first, which automatically triggers cleanup for linked Ralph or UltraQA instances.
   - **Phase 2 (Persistence & Parallelism)**: Shutdown Ralph loops and standalone Ultrawork execution.
   - **Phase 3 (Coordination)**: Terminate Swarm agent coordination and release claimed tasks.
3. **Team Graceful Shutdown**: For native Claude Code Teams, execute a two-pass protocol:
   - **Pass 1 (Graceful)**: Send shutdown requests to all members and wait for confirmation.
   - **Pass 2 (Reconciliation)**: Forcefully remove remaining members and delete the team configuration and task artifacts.
4. **State Cleanup & Preservation**:
   - **Standard Mode**: Remove ephemeral session files while marking Autopilot as inactive to preserve progress for future resumption.
   - **Force Mode**: Iterate through all sessions and legacy JSON artifacts to perform a total workspace reset.
5. **Infrastructure Teardown**: Identify and terminate any associated MCP worker daemons, kill related tmux sessions, and clear heartbeat files to ensure no background processes remain active.

## When to Use
- When the user explicitly requests to "stop," "cancel," or "reset" active OMC operations.
- When an automated stop hook detects that a workflow is complete and requires state cleanup.
- When the workspace state is corrupted or "stale," requiring a forced reset of all sessions and legacy artifacts.
- When transitioning between different execution modes (e.g., switching from a Swarm to a standalone Autopilot) to ensure a clean environment.

## Output
Your response must be structured to provide a clear report of the termination status:

### 1. Cancellation Summary
- **Target Mode**: Identification of the specific mode(s) detected and targeted for cancellation.
- **Action Taken**: Confirmation of whether the cancellation was "Graceful" (progress preserved) or "Force" (state erased).

### 2. Cleanup Details
- **Session Status**: A report on which session-scoped files were removed or updated.
- **Dependency Report**: Status of linked services (e.g., "Ralph shutdown successful, linked Ultrawork cleared").
- **Team Reconciliation**: For team modes, list of members signaled and confirmation of TeamDelete success.

### 3. Workspace Readiness
- **Next Steps**: Guidance on how to resume (if applicable) or confirming that the workspace is now "Fresh" and ready for new commands.
- **Manual Cleanup (If Needed)**: Paths to any artifacts that could not be automatically cleared and require user intervention.
