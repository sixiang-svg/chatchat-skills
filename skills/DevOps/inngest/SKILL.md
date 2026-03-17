---
id: inngest
name: Inngest
description: Design and implement event-driven workflows with Inngest, including function triggers, retries, and observability. Use when building reliable background jobs and orchestrations from application events.
category: DevOps
requires: []
examples:
  - Create an Inngest function triggered by user.signup with idempotent onboarding steps.
  - Add retries, concurrency limits, and alert-ready error metadata to an Inngest workflow.
---

# Inngest

Implement resilient Inngest workflows with explicit event contracts, retry-safe steps, and run-level observability.

## When to Use

- You are implementing async background processing from app events.
- You need retries, delays, fan-out, or step orchestration beyond basic queues.
- You want replayable, debuggable function runs.

## Workflow

1. Define event schema first (name, payload fields, versioning expectations).
2. Create function with a stable trigger and explicit step boundaries.
3. Make each step idempotent and safe to retry.
4. Configure retry strategy, timeout, and concurrency limits per workload.
5. Attach correlation IDs to logs and external calls for run diagnosis.
6. Validate with local/dev replay before production rollout.
7. Roll out with a canary event source or low-volume scope first.

## Concrete Inngest Patterns

**createFunction with trigger/handler.** Use `inngest.createFunction()` with a `name`, `retries`, and `on` trigger. The trigger defines which events invoke the function. Keep function names stable; avoid changing them across deployments as it can break replay and observability.

**step.run for durable steps.** Wrap each unit of work in `step.run()`. Steps are checkpointed; if the function fails, only non-completed steps re-run. Never put multiple side effects in one step unless they are atomic. Use step return values to pass data between steps.

**step.sleep / step.waitForEvent for coordination.** Use `step.sleep()` for delays (e.g., "wait 24 hours"). Use `step.waitForEvent()` to pause until another event arrives (e.g., user confirmation). Both are durable; the function can be paused and resumed without losing state.

**Concurrency limiting.** Set `concurrency.limit` and optionally `concurrency.key` to throttle execution. For high-volume events (e.g., `email.sent`), always set a limit to avoid overwhelming downstream services. Use `concurrency.key` for per-entity or per-tenant limits.

## Common Pitfalls

**Non-idempotent steps causing duplicate side effects.** A step that sends an email or charges a card will run again on retry. Use idempotency keys derived from event data (e.g., `user_id` + `event_id`). Check "already processed" before performing the side effect.

**Missing step boundaries causing full-function retries.** If work is not wrapped in `step.run()`, a failure anywhere retries the entire function. Break work into small steps so only the failed step retries. Large steps also make debugging harder.

**No concurrency limits on high-volume events.** A burst of events can spawn thousands of concurrent runs. Set `concurrency.limit` appropriate to your downstream capacity. Monitor queue depth and run duration.

**Event schema breaking changes without versioning.** Adding required fields or changing types breaks existing producers. Version events (e.g., `user.signup.v2`) or use optional fields with defaults. Document compatibility and migration path.

## Concrete Code Patterns

```typescript
// Function with step boundaries and concurrency
inngest.createFunction(
  {
    id: "onboard-user",
    retries: 3,
    concurrency: { limit: 10 },
    on: { event: "user/signup" },
  },
  async ({ event, step }) => {
    const userId = event.data.user_id;
    await step.run("create-profile", () => createUserProfile(userId));
    await step.run("send-welcome", () => sendWelcomeEmail(userId));
    await step.sleep("wait-24h", "24h");
    await step.run("follow-up", () => sendFollowUpEmail(userId));
  }
);
```

```typescript
// Idempotent side effect with key
await step.run("charge-card", async () => {
  const idempotencyKey = `charge-${event.data.user_id}-${event.id}`;
  const existing = await db.getCharge(idempotencyKey);
  if (existing) return existing;
  const result = await stripe.charge({ ... });
  await db.saveCharge(idempotencyKey, result);
  return result;
});
```

## Output Format

Return:

```markdown
## Event Contract
- Event name: <name>
- Payload: <fields, types, required>
- Version: <if versioned>

## Function Shape
- ID: <function-id>
- Trigger: <event>
- Steps: <list with purpose>
- Retries: <count>
- Concurrency: <limit, key if any>
- Timeout: <seconds>

## Failure Handling
- Idempotency: <strategy per step>
- Compensation: <for partial completion>
- Alerting: <on failure, dead letter>

## Test/Replay Plan
- Local replay: <command or steps>
- Success criteria: <list>
- Canary: <scope, volume>
```

## Constraints

- Do not depend on in-memory state between steps.
- Avoid unbounded fan-out without concurrency limits.
- Never mark a workflow complete when required side effects are unverified.