---
id: wiring
name: Wiring
description: Developer guide for wiring headless features to presentation views using MobX and specific code conventions.
category: Research
requires: []
examples:
  - How do I wire a headless feature to a presentation view using MobX?
  - Explain the code conventions for creating implementations in this admin project.
---

# Admin Developer Guide

## Instruction
- Categorize the new feature as either Headless (reusable business logic) or Presentation (UI-bound logic).
- Create abstractions for Use Cases, Services, and Repositories using `createAbstraction` within the appropriate feature directory.
- Implement features using `createImplementation`, ensuring that the `dependencies` array matches the constructor's injection order.
- Set up stateful classes (Presenters, Repositories) by applying `makeAutoObservable(this)` in the constructor for MobX reactive tracking.
- Wrap all asynchronous state mutations in `runInAction` to comply with strict MobX mutation rules.
- Connect React views to Presenters using the `observer` HOC from `mobx-react-lite` and ensure views only read from the ViewModel (`presenter.vm`).
- Adhere to naming and export conventions, ensuring classes are not exported directly, only the implementation result.

## When to Use
- When developing or refactoring features in a project utilizing the Webiny/MobX architectural pattern.
- When wiring business logic (headless features) to UI components (presentation features) to maintain separation of concerns.
- When needing to ensure consistent dependency injection and reactive state management across a complex admin application.

## Output
- A structured implementation plan following the specific directory and naming conventions.
- Functional code snippets for abstractions, implementations, and MobX-reactive views.
- A checklist of architectural precautions regarding scoping, exports, and state mutation patterns.

## Two Types of Features

### Headless Features

Located under `features/`. No UI. Pure application services — use cases, services, repositories, gateways. Can be injected and invoked from anywhere.

```
features/<domain>/<FeatureName>/
├── abstractions.ts
├── feature.ts
├── <FeatureName>UseCase.ts     # or <FeatureName>Service.ts
├── <FeatureName>Repository.ts
└── <FeatureName>Gateway.ts
```

### Presentation Features

Located under `presentation/`. Contain a Presenter that creates a ViewModel for the React view. May internally compose headless features or own their repo/gateway directly.

```
presentation/<domain>/<FeatureName>/
├── abstractions.ts
├── feature.ts
├── <FeatureName>Presenter.ts
├── <FeatureName>Repository.ts   # only if not reusable
├── <FeatureName>Gateway.ts      # only if not reusable
└── <FeatureName>View.tsx
```

### When to Use Which

- **Reusable logic** (CRUD operations, shared services, anything used by multiple UI areas) → headless feature first, then a presentation feature to wire it to UI.
- **Non-reusable, UI-specific logic** (a single dialog, a config panel) → presentation feature with its own repo/gateway inline.
- **Always**: the React view accesses logic through a presentation feature. Never import a headless feature directly in a React component — wrap it in a presenter or hook.

---

## Headless Features

### Architecture

```
UseCase → Repository → Gateway → External API
```

- **UseCase**: Single application operation. Transient scope (default). Has an `execute()` method.
- **Service**: Stateful, long-lived. Singleton scope. Exposes multiple methods. Uses MobX when observable.
- **Repository**: Owns domain data and cache. Singleton scope.
- **Gateway**: Handles external I/O (GraphQL, REST). Singleton scope.



## Scoping Rules

| Layer | Scope | Rationale |
|---|---|---|
| UseCase | Transient (default) | Fresh per invocation. |
| Service | `.inSingletonScope()` | Long-lived, holds state. |
| Presenter | Transient (default) | One per view instance. Use singleton if shared across views. |
| Repository | `.inSingletonScope()` | One cache instance. |
| Gateway | `.inSingletonScope()` | Stateless but expensive to create. |

---

## Code Conventions

- Use `createAbstraction` from `@webiny/feature/admin` — never `new Abstraction()`.
- All implementations use `createImplementation` with a `dependencies` array matching constructor order.
- Implementation classes are **not exported** — only the `createImplementation` result.
- One class per file. One named export per file.
- One named import per line.
- Use `.js` extensions in all relative imports.
- Use `~` alias for package-internal absolute imports.
- MobX `makeAutoObservable(this)` in every presenter, repository, and service constructor.
- Async state mutations wrapped in `runInAction`.
- Views use `observer` from `mobx-react-lite` and read only from `presenter.vm`.

## Checklist

- [ ] Decided: headless (reusable) or presentation-only (non-reusable)?
- [ ] All abstractions use `createAbstraction`.
- [ ] All implementations use `createImplementation` with correct `dependencies`.
- [ ] Scoping: repos/gateways/services → singleton; use cases/presenters → transient.
- [ ] MobX `makeAutoObservable(this)` in stateful classes.
- [ ] Async state mutations wrapped in `runInAction`.
- [ ] View uses `observer` and reads only from `presenter.vm`.
- [ ] One class per file, one named export per file, one import per line.
- [ ] All relative imports use `.js` extension.
