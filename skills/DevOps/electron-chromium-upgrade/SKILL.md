---
id: electron-chromium-upgrade
name: Electron Chromium Upgrade
description: Plan and deliver Electron/Chromium upgrades with compatibility testing, security review, and rollout safeguards. Use when upgrading desktop app runtime versions to address security, feature, or platform requirements.
category: DevOps
requires: []
examples:
  - Upgrade Electron major version and resolve Chromium API breaks in preload and renderer code.
  - Validate packaging, auto-update, and OS-specific runtime behavior after Chromium security updates.
---

# Electron Chromium Upgrade

Upgrade Electron and bundled Chromium safely by controlling compatibility risk and proving runtime stability before release.

## When to Use

- You need a planned Electron/Chromium version bump for security or platform support.
- Existing app behavior breaks after runtime changes and requires triage.
- You want a release checklist for desktop runtime upgrades.

## Upgrade Techniques

**Electron release notes.** Parse [Electron releases](https://github.com/electron/electron/releases) for breaking changes, deprecations, and security fixes. Check `BREAKING_CHANGES.md` and `CHANGELOG.md`; note Node.js and Chromium versions bundled with each Electron release.

**Breaking change migration.** Follow Electron's migration guides for major bumps (e.g. 28->29). Common areas: `webPreferences` defaults, `contextBridge` usage, `nodeIntegration` and `sandbox` behavior. Align with Chromium's release notes for renderer-impacting changes.

**contextIsolation and sandbox.** Newer Electron defaults enforce `contextIsolation: true` and `sandbox: true`. If your app relied on `contextIsolation: false`, migrate to `contextBridge.exposeInMainWorld` and remove direct `require` in renderer. Ensure preload scripts only expose intended APIs via IPC.

**Preload API migration.** Preload scripts run in an isolated context; they cannot use `require` for arbitrary modules. Use `contextBridge` to expose functions; call `ipcRenderer.invoke` for main-process work. Remove any `window.require` or `process` usage in renderer.

**Node.js version alignment.** Electron bundles a specific Node.js version. Check `process.versions` and update any Node-specific code or native addons. Rebuild native modules with `electron-rebuild` or `npm run rebuild` against the new Electron ABI.

## Testing Strategy

**E2E tests.** Use Playwright (recommended) or Spectron (legacy) to drive the app and assert UI/behavior. Cover: window launch, menu actions, IPC-triggered flows, and critical user paths. Run against the upgraded Electron binary in CI.

**Manual smoke matrix.** Test on each target OS (Windows, macOS, Linux) and architecture (x64, arm64). Verify: cold start, hot reload, file dialogs, system tray, notifications, deep links. Document pass/fail per combination.

**IPC boundary testing.** Exercise all `ipcMain.handle`/`ipcRenderer.invoke` pairs. Ensure context isolation does not break `contextBridge`-exposed APIs. Test preload script load failures and error handling.

## Common Pitfalls

- **Ignoring deprecation warnings.** Warnings from prior versions often become hard errors in the next major. Address deprecations before upgrading.
- **Context isolation breaking preload.** Enabling `contextIsolation` without migrating preload/renderer code causes `require is not defined` or missing globals. Migrate to `contextBridge` and IPC before flipping the flag.
- **Chromium API removals.** Chromium drops APIs periodically (e.g. `document.write`, certain CSS features). Audit renderer code and third-party scripts for removed or changed APIs.
- **Native module binary compatibility.** Native addons (e.g. `node-sqlite3`, `sharp`) must be rebuilt for the new Electron ABI. Use `electron-rebuild`; verify no ABI mismatch crashes on startup.

## Workflow

1. Select target Electron version and review upstream breaking changes.
2. Inventory impact areas:
   - Node/Electron APIs in main process
   - Preload context isolation and IPC contracts
   - Renderer/browser behavior tied to Chromium changes
3. Upgrade dependencies and lockfile in a dedicated branch.
4. Run platform matrix tests (Windows/macOS/Linux as applicable).
5. Validate signing, packaging, installer, and auto-update flows.
6. Perform smoke tests for startup, auth/session, file access, and critical user journeys.
7. Ship with staged rollout and crash/error telemetry monitoring.

## Output Format

Return:

- **Target/runtime rationale:** Chosen Electron version, bundled Node/Chromium versions, security or feature drivers, and risk level (low/medium/high).
- **Breaking-change impact map:** Table of affected areas (main, preload, renderer, native modules), change type, mitigation status, and owner.
- **Cross-platform validation:** Matrix of OS x architecture with E2E pass/fail, smoke test results, and IPC boundary verification.
- **Rollout and rollback recommendation:** Staged rollout plan, telemetry thresholds, rollback triggers, and rollback steps (downgrade version, revert manifest).

## Constraints

- Do not skip cross-platform checks for desktop-distributed apps.
- Avoid mixing major runtime upgrade with unrelated feature refactors.
- Keep IPC boundary hardening (contextIsolation/sandbox) intact during migration.
- Require crash-rate monitoring before full rollout.