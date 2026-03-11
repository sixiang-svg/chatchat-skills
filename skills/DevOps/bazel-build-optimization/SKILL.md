---
id: bazel-build-optimization
name: Bazel Build Optimization
description: Build-system optimization playbook for reducing Bazel build times and improving cache effectiveness.
category: DevOps
requires: []
examples:
  - "Analyze this Bazel project and propose the highest-impact build speed improvements."
  - "Our CI Bazel builds regressed; provide a targeted optimization workflow."
---

# Bazel Build Optimization

Use this skill to diagnose Bazel performance bottlenecks and apply measurable optimizations.

## When to Use

- Local or CI builds are too slow or unstable.
- Cache hit rate is low despite repeated builds.
- Incremental builds rebuild too many unrelated targets.

## Workflow

1. **Capture baseline metrics**: Run clean build, incremental build (touch one file), and repeated build. Record wall time, critical path, and cache hit/miss counts. Use `bazel build --profile=profile.json //...` to generate a profile; inspect with `bazel analyze-profile profile.json` or Chrome trace viewer.

2. **Identify expensive targets and actions**: Enable Build Event Protocol with `--build_event_json_file=events.json` or `--build_event_binary_file=events.bep`. Use `bazel aquery 'deps(//target)' --output=text` to inspect action graph. Run `bazel query 'rdeps(//..., //changed:target)'` to see what a change invalidates. Focus on critical path actions and high-fanout targets.

3. **Reduce invalidation**: Replace broad `glob(["**/*.java"])` with explicit file lists or narrow patterns. Isolate generated outputs in dedicated packages. Use `--experimental_inmemory_dotd_files` and `--experimental_inmemory_jdeps_files` where supported to avoid disk I/O. Prefer `filegroup` with explicit `srcs` over transitive globs.

4. **Improve cacheability**: Ensure all actions are hermetic (no host paths, timestamps, or non-deterministic tools). Use `--stamp` only when required for release builds. Prefer `rules_*` over custom `genrule`; if using `genrule`, declare all inputs explicitly and avoid shell commands that read environment or host state. Use deterministic toolchains and lock down tool versions.

5. **Optimize remote execution and caching**: Configure `--remote_executor` and `--remote_cache` in `.bazelrc` with appropriate flags. Use `--remote_download_minimal` or `--remote_download_toplevel` to reduce download overhead. Tune `--jobs` and `--local_ram_resources` for your machine. Ensure CI and local use the same platform and toolchain config for cache hits.

6. **Re-measure**: After each change, run the same build sequence and compare. Keep only changes with statistically meaningful improvement. Document methodology so others can reproduce.

## Common Pitfalls

- **Broad globs invalidating cache**: `glob(["**/*"])` or `glob(["*.ext"])` across large trees causes Bazel to re-evaluate on any file addition/removal, invalidating downstream actions. Prefer explicit `srcs` or narrow patterns.

- **Non-hermetic actions**: Actions that depend on host paths, `$HOME`, timestamps, or non-declared inputs produce different digests across machines and break cache. Audit with `bazel aquery` and ensure all inputs are declared.

- **Genrule misuse**: `genrule` with complex shell, multiple outputs, or undeclared dependencies is a common source of cache misses and non-determinism. Migrate to Starlark rules or use `ctx.actions.run` with explicit inputs/outputs.

- **Action cache vs repository cache**: Action cache stores action outputs keyed by input digest; repository cache stores external dependency fetches. Low action cache hit rate with good repo cache suggests hermeticity or input declaration issues. Check `--remote_cache` and `--repository_cache` separately.

## Profiling and Diagnosis Commands

```bash
# Generate profile and analyze
bazel build --profile=profile.json //...
bazel analyze-profile profile.json

# Build event protocol for detailed timing
bazel build --build_event_json_file=events.json //...

# Query dependency graph
bazel query 'deps(//target)' --output=graph
bazel query 'rdeps(//..., //changed)' --output=label

# Action graph analysis
bazel aquery 'deps(//target)' --output=text

# Check what a file change affects
bazel query "rdeps(//..., //path/to:target)"
```

## Remote Cache vs Remote Execution

| Use remote cache when | Use remote execution when |
|-----------------------|----------------------------|
| Local machines have sufficient CPU/RAM | Local resources are constrained |
| Build graph is moderate; actions are the bottleneck | Many actions run in parallel; local parallelism is limited |
| Team is small; cache warming is manageable | Large team; cache is pre-warmed by others |
| Network latency to cache is acceptable | Need to offload work entirely |

Start with remote cache only; add remote execution if action execution (not analysis) dominates and local parallelism is saturated. Ensure `--remote_default_exec_properties` and platform config match between local and CI for cache reuse.

## Output / Checklist

- **Before/after metrics**: Clean build time, incremental build time, cache hit rate (action and repository), critical path duration. Include exact commands and environment (Bazel version, `--config`, machine specs).

- **Ranked optimizations**: List changes by impact (time saved) and implementation cost (LOC, risk). Prioritize high-impact, low-cost items.

- **Risks and rollback**: Note which changes affect build correctness or reproducibility. Document how to revert (e.g., `.bazelrc` flags, rule changes).

- **Follow-up monitoring**: Define a regression test (e.g., nightly benchmark, CI job that fails on N% slowdown). Specify who owns it and how to triage.

## Constraints

- Do not trade correctness for speed.
- Avoid large-scale rule rewrites without metrics-backed justification.
- Keep local and CI behavior aligned to prevent false gains.
- Do not recommend disabling sandboxing or hermeticity for performance without explicit security trade-off acknowledgment.