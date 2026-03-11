---
id: fixing-streamlit-ci
name: Fixing Streamlit CI
description: Diagnose and repair Streamlit CI pipeline failures with reproducible checks for dependencies, tests, and deployment packaging. Use when GitHub-based Streamlit workflows fail in pull requests or mainline builds.
category: DevOps
requires:
  - github
examples:
  - Fix a GitHub Actions Streamlit build failing due to dependency resolution or Python version mismatch.
  - Stabilize flaky Streamlit CI by separating lint/test/package stages with deterministic caching.
---

# Fixing Streamlit CI

Restore Streamlit CI health quickly, then harden the pipeline to prevent repeat failures.

## When to Use

- A Streamlit workflow fails on pull requests or protected branches.
- You need to isolate whether failures come from environment, tests, packaging, or deployment steps.
- You want a standard remediation flow with evidence and rollback-safe changes.

## Workflow

1. **Reproduce the failure**
   - Use `act` to run the workflow locally against the failing commit.
   - Add `workflow_dispatch` to the workflow so you can trigger manual runs with branch/ref overrides.
   - Capture artifacts from failed runs: logs, pip list output, and any tracebacks before the job ends.
   - Run in a fresh venv matching the CI Python version; avoid relying on your local environment.

2. **Classify failure type**
   - Dependency/install: pip resolver conflicts, missing extras, lockfile drift.
   - Test/runtime: cache decorator issues, component import failures, headless mode gaps.
   - Build/package: wheel/sdist build errors, missing manifest entries.
   - Deployment/authentication: secrets, tokens, or cloud provider auth.

3. **Validate dependencies**
   - Resolve conflicting pins: ensure `streamlit`, `protobuf`, `grpcio`, and `typing-extensions` versions align across requirements.txt, pyproject.toml, or poetry.lock.
   - If using Poetry or PDM, verify lockfile is committed and CI uses `poetry install --sync` or equivalent; avoid `pip install .` without a lockfile.
   - Check for missing extras (e.g., `streamlit[plotly]`) if the app uses optional integrations.
   - Pin `protobuf` explicitly if you see `TypeError` or `AttributeError` from protobuf; Streamlit is sensitive to protobuf major versions.

4. **Validate Streamlit runtime**
   - Run `streamlit run app.py --server.headless true` locally; headless mode is closer to CI.
   - Test `st.cache_data` vs `st.cache_resource` usage: ensure TTL and hashing are compatible with your Python version.
   - Verify custom components import without `npm`/Node in CI; prebuild wheels or skip component tests if Node isn't available.

5. **Check cache and determinism**
   - Use cache keys that include Python version, lockfile hash, and OS (e.g., `${{ runner.os }}-py-${{ matrix.python }}-${{ hashFiles('**/poetry.lock') }}`).
   - Invalidate cache when changing dependency files; avoid overly broad keys that hide stale installs.

6. **Split and observe pipeline stages**
   - Separate lint, test, package, and deploy into distinct jobs with clear failure points.
   - Add `continue-on-error: false` where appropriate so one stage failing doesn't silently pass others.

7. **Add smoke tests**
   - Run `streamlit run app.py --server.headless true` with a short timeout; assert exit code 0 or that the process starts and responds.
   - Avoid relying only on unit tests that mock Streamlit; the real runtime can fail on import or first render.

8. **Re-run and confirm**
   - Trigger CI after each change; do not batch multiple fixes without verifying each.

## Common Pitfalls

- **Pinning Streamlit but not protobuf**: Streamlit pulls protobuf as a dependency; a newer protobuf can break compatibility. Pin both in requirements or lockfile.
- **Ignoring deprecation warnings**: Warnings in Streamlit (e.g., `st.cache` -> `st.cache_data`) can become errors in the next minor release. Fix warnings before they block CI.
- **Testing with `streamlit run` without headless mode**: Non-headless runs may behave differently in CI; always use `--server.headless true` for CI-like validation.
- **Single-stage pipelines**: Lumping install, test, and deploy into one job makes it hard to know where failure occurred. Split stages.
- **No lockfile or loose pins**: `streamlit>=1.28` in requirements.txt can resolve to different versions across runs. Use a lockfile or exact pins.

## Diagnosis Decision Tree

| Error type | Look first |
|------------|------------|
| `ModuleNotFoundError`, `ImportError` | Dependencies step; missing package or wrong Python version. Check `pip list` / `poetry show`. |
| `TypeError` or `AttributeError` involving protobuf/grpc | Pin `protobuf` and `grpcio`; check Streamlit release notes for compatible versions. |
| `streamlit run` hangs or times out | Add `--server.headless true`; ensure no interactive prompts or blocking I/O. |
| Custom component fails to load | Verify Node/npm in CI or use prebuilt component; check `streamlit components` path. |
| Flaky or environment-dependent failures | Cache key too broad or missing; lockfile not used; Python version mismatch. |
| Deployment/auth errors | Secrets, env vars, and cloud CLI config; verify `secrets` context and token scopes. |

## Output Format

When reporting findings, structure output as:

1. **Root cause**: One-line summary (e.g., "protobuf 5.x incompatible with streamlit 1.28").
2. **Evidence**: Exact error message, failing step name, and relevant log snippet (sanitized).
3. **Fix**: Concrete change (file, line, before/after).
4. **Verification**: Command or step to confirm the fix (e.g., "Re-run `test` job on PR #N").
5. **Prevention**: Optional hardening (e.g., "Add protobuf pin to requirements.txt").

## CI Repair Checklist

- [ ] Failure reproduced or confidently isolated.
- [ ] Dependency graph is pinned and install is deterministic.
- [ ] Test and packaging stages are separable and observable.
- [ ] Smoke check verifies Streamlit app startup path.
- [ ] Protobuf and Streamlit versions are compatible and pinned.
- [ ] Headless mode used for any `streamlit run` in CI.

## Constraints

- Do not merge with flaky status checks still unresolved.
- Avoid adding broad retry loops that hide underlying instability.
- Keep secrets masked and never print credentials in CI logs.
- Prefer small, auditable workflow changes over large rewrites.
- Do not remove or weaken existing pins without verifying compatibility.
- Do not run `streamlit run` in CI without `--server.headless true`.
- Preserve lockfile integrity; do not regenerate lockfiles without explicit user intent.