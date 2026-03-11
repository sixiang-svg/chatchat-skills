---
id: bats-testing-patterns
name: Bats Testing Patterns
description: Practical patterns for writing maintainable Bats tests in shell-heavy CI and release pipelines.
category: DevOps
requires: []
examples:
  - "Create Bats tests for this deploy script with reliable setup and teardown."
  - "Refactor flaky Bats tests into deterministic patterns."
---

# Bats Testing Patterns

Use this skill to design stable, readable Bats tests for scripts, CLIs, and automation tasks.

## When to Use

- You are adding tests for shell scripts used in CI/CD.
- Existing Bats tests are flaky or difficult to debug.
- You need reusable fixtures for filesystem, env vars, or command mocks.

## Concrete Bats Patterns

**Setup and teardown:** Use `setup()` and `teardown()` functions. Bats runs them before and after each test. Create temp dirs in setup, remove them in teardown. Reset env vars to avoid leakage.

**Load helpers:** `load 'test_helper/bats-support/load'` and `load 'test_helper/bats-assert/load'` for `assert_success`, `assert_failure`, `assert_output`, `refute_output`. Or define custom helpers in a `test_helper.bash` and `load '../test_helper'`.

**@test annotations:** Each test is a function prefixed with `@test "description"`. Example: `@test "exits 0 when config is valid" { run ./script.sh; assert_success; }`.

**Run and assertions:** `run ./script.sh arg1 arg2` captures exit code in `$status`, stdout in `$output`, stderr in `$stderr`. Use `assert_success` (status 0), `assert_failure` (non-zero), `assert_output --partial "expected"`, `assert_output - "exact"`, `assert_line "line"`. For line-by-line: `assert_line -n 1 "first line"`.

## Fixture Management

**Temp directories:** Use `BATS_TMPDIR` or `mktemp -d`. Create test data under it. Clean in teardown: `rm -rf "$BATS_TMPDIR/mytest"`. Avoid `/tmp` directly; use project-scoped paths.

**Command mocking:** Override commands with functions. Example: `curl() { echo '{"ok":true}'; }` then `export -f curl`. Or use `stub` from bats-mock if available. Restore in teardown: `unset -f curl` or source original script.

**Sample files:** Create fixture files in setup: `echo "content" > "$BATS_TMPDIR/fixture.txt"`. Reference via `$BATS_TMPDIR/fixture.txt` in tests.

## Common Pitfalls

- **Not quoting variables:** Use `"$var"` everywhere. Unquoted vars break on spaces and empty values.
- **Relying on host-installed tools:** Ensure required commands exist: `command -v jq >/dev/null || skip "jq required"`. Prefer portable constructs.
- **Missing cleanup on failure:** Teardown runs even when tests fail. Use `trap` for critical cleanup: `trap 'rm -rf "$TMP"' EXIT`.
- **Test ordering dependencies:** Each test must be independent. Do not assume another test ran first. Reset state in setup.

## Concrete Bats Test Examples

```bash
setup() {
  load '../test_helper'
  FIXTURE_DIR="$(mktemp -d)"
}

teardown() {
  rm -rf "$FIXTURE_DIR"
}

@test "deploy script succeeds with valid config" {
  cp fixtures/valid.yaml "$FIXTURE_DIR/config.yaml"
  run ./deploy.sh --config "$FIXTURE_DIR/config.yaml"
  assert_success
  assert_output --partial "Deployment complete"
}

@test "deploy script fails when config missing" {
  run ./deploy.sh --config /nonexistent
  assert_failure
  assert_output --partial "config not found"
}
```

## Workflow

1. Define test scope by behavior: success paths, failure paths, and side effects.
2. Build fixture helpers for temp directories, sample inputs, and common assertions.
3. Isolate external dependencies using command stubs and deterministic environment setup.
4. Write small tests with clear assertions on exit status, stdout/stderr, and file outputs.
5. Add teardown cleanup and leak checks to avoid cross-test contamination.
6. Run tests in CI-like environment and fix nondeterministic assumptions.

## Output Format

```markdown
## Bats Suite Structure
- File layout: <test files and helper locations>
- Setup/teardown: <what is created and cleaned>

## Test Cases
| Test | Behavior | Assertions |
|------|----------|------------|
| <name> | <description> | status, output, files |

## Fixtures
- Temp dir: <BATS_TMPDIR or mktemp usage>
- Mocks: <command overrides>
- Sample files: <paths and content>

## Pitfall Checklist
- [ ] Variables quoted
- [ ] No host-tool assumptions without skip
- [ ] Teardown cleans all state
- [ ] Tests independent

## Flake-Reduction Notes
- Timing assumptions removed
- State reset between tests
- CI execution guidance and runtime constraints
```

## Constraints

- Avoid network and wall-clock dependencies unless explicitly mocked.
- Keep tests portable across developer machines and CI runners.
- Assert behavior, not exact implementation details where possible.