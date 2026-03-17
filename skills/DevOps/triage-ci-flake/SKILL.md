---
id: triage-ci-flake
name: Triage CI Flake
description: Triage flaky CI failures by classifying root causes, isolating unstable tests/jobs, and driving targeted reliability fixes.
category: DevOps
requires: []
examples:
  - Triage this flaky CI failure and suggest the most likely root cause.
  - Build a remediation plan to reduce recurring flaky test failures.
---

# Triage CI Flake

Investigate intermittent CI failures and convert them into actionable fixes.

## When to Use

- CI fails intermittently with non-deterministic behavior.
- You need to separate infra flakes from test logic issues.
- You want to reduce re-runs and unblock developer flow.

## Workflow

1. **Capture flaky failure signature and recurrence rate**
   - Record exact error message, stack trace, and exit code.
   - Note job name, test path, and branch/commit.
   - Compute failure rate over last N runs (e.g., 5/20 = 25%).
   - Capture timestamps and parallel job ordering if available.
   - Store artifact URLs (logs, screenshots) for reproducibility.

2. **Group flakes by probable cause**
   - **Timing**: Assertions before async completion; missing waits; race between setup and test.
   - **Shared state**: Tests mutating global fixtures; DB/cache not reset; file system pollution.
   - **Network dependencies**: External APIs, CDNs, or package registries; timeouts or rate limits.
   - **Resource contention**: Memory, CPU, or disk pressure; parallel jobs competing for same resources.
   - **Non-deterministic ordering**: Map/Set iteration order; parallel test execution order; random seed not fixed.

3. **Reproduce under controlled conditions**
   - Run the failing test in isolation with `--repeat-each=N` or equivalent.
   - Disable parallelization to rule out ordering effects.
   - Use same runner type (e.g., same GitHub Actions runner image) as prod.
   - Inject delays or network failures to stress timing paths.

4. **Prioritize fix candidates by frequency and impact**
   - High-frequency flakes (>10%) block more developers; fix first.
   - Critical path tests (e.g., deploy gates) outweigh low-traffic unit tests.
   - Prefer root-cause fixes over retries or quarantine.

5. **Verify recurrence drop after remediation**
   - Run the previously flaky test 50+ times in CI before closing.
   - Monitor for 1-2 weeks; some flakes have long tails.

## Flake Classification Guide

| Category | Indicators | Investigation Strategy |
|----------|------------|-------------------------|
| **Timing** | Timeouts, "element not found", assertions on async state | Add explicit waits; increase timeout only after confirming it's not masking a bug; use deterministic completion signals |
| **Shared state** | Failures only when tests run together; order-dependent | Isolate fixtures per test; use transactional rollback or fresh DB per test; avoid static/global mutable state |
| **Network** | Connection refused, 5xx, DNS failures, rate limit errors | Mock external services; use hermetic fixtures; add retries only for transient infra, not for app bugs |
| **Resource** | OOM, disk full, "too many open files" | Reduce parallelism; increase resource limits; fix leaks instead of increasing limits |
| **Ordering** | Failures change when test order changes | Fix random seed; run tests in deterministic order; avoid tests that depend on execution order |

## Common Pitfalls

- **Blanket retries hiding real bugs**: Retrying every failure masks underlying issues. Use retries only for known transient infra (e.g., network blips) and cap at 1-2 retries. If a test needs >2 retries to pass, fix the root cause.
- **Quarantining without follow-up**: Marking tests as "skip" or "quarantine" without a ticket or SLA leads to permanent debt. Every quarantined test must have an owner and a target date for fix or removal.
- **Fixing symptoms instead of causes**: Increasing timeouts or adding sleeps often papers over races. Prefer explicit synchronization, deterministic completion, or test redesign.
- **Ignoring recurrence rate**: A 2% flake can still block 1 in 50 PRs. Track and triage by impact (PRs blocked x frequency), not just raw failure count.
- **Treating all flakes alike**: Infra flakes (runner OOM, network) need different fixes than test logic flakes. Misclassifying leads to wrong remediation.

## Output Format

```markdown
## Flake Profile
- **Job/test**: <full job name and test path>
- **Failure signature**: <exact error message, exception type, first 3 lines of stack trace>
- **Recurrence**: <X failures / Y runs> (<Z%>) over <time window>
- **Artifacts**: <links to logs, screenshots, or build artifacts>
- **Suspected category**: <from classification guide>

## Likely Causes (ranked)
1. <cause> - <brief evidence>
2. <cause> - <brief evidence>

## Remediation Plan
- [ ] <specific action, e.g., "Add explicit wait for element X before assertion">
- [ ] <deterministic guard, e.g., "Reset DB in beforeEach">
- [ ] Track recurrence for N runs (recommend N >= 50)
- [ ] Owner: <person or team> | Target: <date>

## Constraints
- Do not add retries without identifying the transient cause.
- Do not quarantine without a follow-up ticket and owner.
- Prefer root-cause fixes over timeouts or sleeps.
```

## Constraints

- **No blind retries**: Retries must be scoped to a known transient failure mode (e.g., network timeout). Reasoning: Unbounded retries hide real bugs and slow CI.
- **No permanent quarantine**: Every skipped test needs an owner and remediation plan. Reasoning: Orphaned quarantines accumulate and erode test suite trust.
- **Reproduce before fixing**: Attempt reproduction (isolated run, repeat-each) before applying fixes. Reasoning: Fixing without reproduction risks addressing the wrong cause.
- **Capture before closing**: Document failure signature and recurrence in the fix PR. Reasoning: Enables future correlation if the flake resurfaces.