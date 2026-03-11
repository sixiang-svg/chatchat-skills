---
id: workflow-patterns
name: Workflow Patterns
description: Define reusable DevOps workflow patterns for planning, execution, validation, and handoff across engineering teams.
category: DevOps
requires: []
examples:
  - Propose a reusable workflow pattern for this release process.
  - Build a standard execution checklist for this DevOps task.
---

# Workflow Patterns

Create practical workflow templates that improve consistency and reduce execution risk.

## When to Use

- You need a repeatable process for recurring DevOps work.
- You want clear ownership, gates, and success criteria.
- You need handoff-ready documentation for team execution.

## Workflow

1. **Define workflow goal, scope, and trigger condition.** State the outcome, who is responsible, and what event starts the workflow (e.g., merge to main, P1 incident, on-call shift start).

2. **Apply trigger-action-verify loops.** Each stage should: trigger on an input or gate, perform an action, then verify the outcome before moving on. Never skip verification.

3. **Break work into stages with explicit inputs and outputs.** Each stage has: owner, inputs (artifacts, approvals), actions, outputs (artifacts, status), and success criteria.

4. **Add stage gates.** Gates are explicit checkpoints where work stops until conditions are met. Example: "No deploy until all tests pass and change advisory is approved."

5. **Define escalation paths.** For each failure mode, specify: who is notified, escalation timeout, and next step (retry, escalate, rollback).

6. **Assign owners and escalation rules.** Every stage has a single owner. Escalation goes to the next level (e.g., on-call -> tech lead -> manager) with clear timeouts.

7. **Package workflow as a reusable template.** Include: checklist, runbook links, decision trees, and rollback instructions.

## Common Pitfalls

- **Over-engineering workflows.** Avoid adding stages for rare edge cases. Start minimal; extend only when a failure occurs.

- **Missing rollback paths.** Every deploy or risky change must have a documented rollback procedure. Test it periodically.

- **Unclear ownership.** "The team" is not an owner. Assign a named role or person per stage.

- **Implicit gates.** Gates must be explicit (e.g., "Approval from X required") and enforceable, not assumed.

- **No escalation timeouts.** Escalation without a defined timeout leads to delays. Use SLOs (e.g., "Escalate if no response in 15 minutes").

- **Skipping verification.** Action without verification creates false confidence. Every stage needs a verification step.

## Example Workflow Patterns

**Release workflow:** Trigger -> merge to release branch. Stages: build -> test -> stage deploy -> smoke test -> production deploy (manual gate) -> post-deploy verification. Rollback: revert commit + redeploy previous tag. Escalation: release manager -> engineering manager.

**Incident response workflow:** Trigger -> P1/P2 alert. Stages: acknowledge (on-call) -> triage (identify scope) -> mitigate (fix or rollback) -> verify (monitoring stable) -> post-mortem. Escalation: on-call -> secondary -> tech lead -> manager. Timeouts: 5 min acknowledge, 15 min escalate.

**On-call rotation handoff:** Trigger -> shift start. Stages: receive handoff (incidents, context) -> verify access (dashboards, runbooks) -> confirm with outgoing on-call -> assume ownership. Output: handoff checklist signed, escalation contacts updated.

## Output Format

```markdown
## Workflow Summary
- Goal: <outcome>
- Trigger: <when to run>
- Owner: <primary role>

## Stages
1. <stage name>
   - Owner: <role>
   - Input: <what is required>
   - Action: <what to do>
   - Verify: <how to confirm success>
   - Output: <artifact or status>

## Stage Gates
- [ ] Stage 1: <precondition>
- [ ] Stage 2: <precondition>

## Escalation Path
- Level 1: <role> - timeout: <duration>
- Level 2: <role> - timeout: <duration>

## Rollback Path
- <steps to rollback>

## Validation Gates
- [ ] Preconditions met
- [ ] Stage checks passed
- [ ] Final verification complete
```

## Constraints

- Prefer explicit gates over implicit assumptions.
- Keep each stage small and testable.
- Include rollback or fallback steps for risky stages.
- Every stage has a single owner and a verification step.
- Define escalation paths with timeouts; avoid vague "escalate if needed."
- Use trigger-action-verify loops; never skip verification.
- Document rollback paths for all deploy or change workflows.