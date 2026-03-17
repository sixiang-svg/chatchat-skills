---
id: monorepo-management
name: Monorepo Management
description: Manage monorepo workflows for build performance, dependency boundaries, release coordination, and developer productivity.
category: DevOps
requires: []
examples:
  - Propose a monorepo strategy to improve CI speed and ownership boundaries.
  - Create a plan for scalable dependency and release management in this monorepo.
---

# Monorepo Management

Design maintainable monorepo operating patterns for scale and reliability.

## When to Use

- You need to improve monorepo build/test/release workflows.
- You want clearer package boundaries and ownership rules.
- You need to reduce CI cost and developer wait time.

## Workflow

1. **Map repository structure and dependency graph hotspots.** Use tools like `madge`, `dependency-cruiser`, or `nx graph` to visualize the dependency graph. Identify cycles, deep dependency chains, and packages with high fan-out. Document which packages are shared infrastructure vs. domain-specific.

2. **Define ownership and change-impact boundaries.** Use `CODEOWNERS` to enforce who can approve changes to each package or directory. Pair with branch protection so changes to `packages/core/*` require approval from the core team. Define allowed dependency directions (e.g., `packages/app` may depend on `packages/ui` but not vice versa) and enforce via lint rules or `dependency-cruiser`.

3. **Optimize build/test with caching and selective execution.** Adopt a workspace protocol (npm workspaces, Yarn workspaces, or pnpm workspaces) for consistent installs and hoisting. Use affected-only CI: Nx (`nx affected`), Turborepo (`turbo run build --filter=...[origin/main]`), or Bazel to run builds and tests only for packages touched by a PR. Enable remote caching (Nx Cloud, Turborepo Remote Cache, or Bazel remote cache) so CI and local runs share artifacts.

4. **Define release/versioning strategy for packages/services.** Use Changesets or Lerna for coordinated versioning: developers add a changeset file describing the change and version bump type; a release workflow batches changesets and publishes. For independent packages, consider independent versioning; for tightly coupled packages, use fixed versioning. Never publish from unstable branches; publish only from `main` or a dedicated release branch after merge.

5. **Add governance checks for dependency and API contract stability.** Run `dependency-cruiser` or custom rules in CI to block new circular dependencies or violations of layering. Use API extractors or similar tools to detect breaking changes in public APIs before merge.

## Dependency Graph Management and Selective Test Execution

- **Layering rules:** Define layers (e.g., `packages/core` -> `packages/domain` -> `packages/app`) and enforce that lower layers never import from higher layers. Use `dependency-cruiser` rules like `forbidden` to block violations.
- **Affected detection:** Base affected set on git diff against the target branch. Include transitive dependents if a package's public API changed. For tests, run unit tests only in affected packages; run integration/e2e tests when shared infra or entry points change.
- **Caching keys:** Include lockfile hash, package.json hashes of dependencies, and source hashes. Invalidate when any of these change. Use content-addressable caching where possible.

## Common Pitfalls

- **Running all tests on every PR.** This scales poorly. Use affected-only execution and tier tests: fast unit tests per package, slower integration tests only when affected.
- **Circular dependencies between packages.** These cause subtle build order issues and runtime problems. Detect early with tooling and break cycles by extracting shared code into a new package or inverting the dependency.
- **Inconsistent tooling versions across packages.** Different Node versions, TypeScript versions, or ESLint configs lead to flaky builds and confusion. Pin versions at the root and use a single lockfile. Consider `volta` or `nvm` for Node version consistency.
- **Publishing from unstable branches.** Publishing from feature branches or long-lived release branches can pollute the registry and confuse consumers. Publish only from `main` (or a release branch) after changes are merged and validated.

## Output Format

```markdown
## Monorepo Assessment
- Current pain points: <list with severity>
- High-impact boundaries: <list with rationale>
- Dependency graph summary: <cycle count, max depth, shared package count>
- Tooling inventory: <package manager, build system, current CI approach>

## Optimization Plan
- CI/runtime improvements:
  - Workspace protocol: <npm|yarn|pnpm> workspaces
  - Affected-only execution: <Nx|Turborepo|Bazel> with filter/affected commands
  - Remote caching: <yes|no, provider>
  - Selective test tiers: <unit scope, integration scope, e2e triggers>
- Ownership rules:
  - CODEOWNERS paths and teams
  - Allowed dependency directions (layering)
  - Branch protection for shared packages
- Release model: <changeset|lerna|independent|fixed>
- Governance: <dependency-cruiser rules, API contract checks>

## Dependency and Test Patterns
- Layering: <layer names and allowed directions>
- Affected detection: <git diff base, transitive dependent inclusion>
- Cache invalidation: <key components>

## Success Metrics
- [ ] CI duration reduction target (e.g., <X min for typical PR>
- [ ] Flake/error reduction target
- [ ] Developer throughput indicator (e.g., PR merge time)
- [ ] Zero circular dependencies, layering violations blocked
```

## Constraints

- Do not run full test suites on every PR; use affected-only execution.
- Enforce dependency boundaries with tooling, not documentation alone.
- Pin tooling versions at the root; avoid per-package drift.
- Publish only from stable branches after merge.
- Prefer a single lockfile and workspace protocol for reproducible installs.
