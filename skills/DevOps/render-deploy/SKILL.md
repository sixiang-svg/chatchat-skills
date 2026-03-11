---
id: render-deploy
name: Render Deploy
description: Plan and execute Render deployments with environment validation, health checks, and clear rollback conditions.
category: DevOps
requires: []
examples:
  - Help me deploy this service on Render with a safe rollout plan.
  - Build a Render deployment checklist with post-deploy verification steps.
---

# Render Deploy

Deploy to Render reliably with preflight checks and service-health verification.

## When to Use

- You are deploying a new release to Render.
- You need to reduce release risk for web/background services.
- You want explicit success and rollback criteria.

## Workflow

1. **Confirm service type, runtime, and deployment target.** Identify whether the service is a Web Service, Background Worker, or Cron Job. Specify the region and plan tier (free, starter, standard). Decide between auto-deploy (triggered on git push) and manual deploy for production; prefer manual deploy for production to control timing and avoid accidental releases.

2. **Validate environment variables and dependent services.** Ensure all required env vars are set in the Render dashboard or via `render.yaml`. Confirm private services and databases are reachable. Use environment groups for staging vs production to avoid cross-environment leakage.

3. **Configure build and deploy behavior.** Set explicit `buildCommand` and `startCommand` in `render.yaml` or the dashboard; never rely on Render's auto-detection for production. Use build filters (e.g., `branch: main` or path filters) to avoid unnecessary builds. For preview environments, configure branch-based deploys with unique URLs.

4. **Define health check and startup behavior.** Configure a dedicated health check path (e.g., `/health`) that returns 200 and exercises minimal logic. Set `healthCheckPath`, `healthCheckInterval`, and `unhealthyThreshold` appropriately. Free-tier services spin down after inactivity; document cold start latency and consider a warm-up strategy for user-facing endpoints.

5. **Handle disk and persistent storage.** Render's filesystem is ephemeral except for mounted disks. If the app writes logs, uploads, or cache to disk, configure a persistent disk and mount path. Never assume `/tmp` or project directories persist across deploys or restarts.

6. **Deploy and monitor startup and health signals.** Trigger deploy (manual or via push), watch build logs for failures, then monitor the health check and startup logs. Confirm the service reaches "Live" before declaring success.

7. **Apply rollback if checks fail or regressions appear.** Use Render's Deploy History (Dashboard -> Service -> Deployments) to roll back. Select the previous successful deploy and click "Rollback" or "Redeploy." Document the rollback trigger and capture incident notes for post-mortem.

## Common Pitfalls

- **Relying on auto-deploy for production.** Auto-deploy on `main` can ship broken commits. Use manual deploy or branch protection plus deploy hooks for production.
- **Not configuring a health check path.** Without `healthCheckPath`, Render cannot reliably detect unhealthy instances; traffic may still route to failing containers.
- **Missing build command in render.yaml.** If `buildCommand` is omitted, Render may guess incorrectly (e.g., wrong package manager or no build step), leading to failed or incomplete deploys.
- **Ignoring cold start behavior on free tier.** Free services sleep after inactivity; first requests can take 30-60+ seconds. Set user expectations or use a paid plan for production.
- **Ephemeral filesystem assumptions.** Writing to the project directory or `/tmp` without a persistent disk means data is lost on restart or redeploy. Use Render Disks for persistent storage.

## render.yaml Configuration Patterns

```yaml
services:
  - type: web
    name: my-api
    runtime: node
    region: oregon
    plan: starter
    buildCommand: npm ci && npm run build
    startCommand: npm run start
    healthCheckPath: /health
    envVars:
      - key: NODE_ENV
        value: production
    disk:
      name: data
      mountPath: /data
      sizeGB: 1
```

For preview environments, use `branch` and `autoDeploy`:

```yaml
services:
  - type: web
    name: my-api-preview
    branch: develop
    autoDeploy: true
    buildCommand: npm ci && npm run build
    startCommand: npm run start
    healthCheckPath: /health
```

## Rollback Guidance

Render stores deploy history per service. To roll back: open the service -> Deployments -> select the last known-good deploy -> Rollback/Redeploy. The previous deploy's image and config are reused. There is no built-in blue-green or canary; rollback is full revert to a prior deploy.

## Output Format

```markdown
## Deployment Plan
- Service: <name>
- Target: <env>
- Change scope: <summary>
- Deploy mode: auto-deploy | manual
- Health check path: <path>

## Preflight Checklist
- [ ] Runtime/build config validated (buildCommand, startCommand in render.yaml)
- [ ] Environment variables validated
- [ ] Dependency readiness confirmed
- [ ] Health check path configured and tested
- [ ] Persistent disk configured if app writes to filesystem

## Verification
- [ ] Health endpoint passes
- [ ] Core user flow passes
- [ ] Logs and error rate normal
- [ ] Cold start latency acceptable (if free tier)

## Rollback
- Trigger: <condition>
- Action: Dashboard -> Service -> Deployments -> select prior deploy -> Rollback
- Notes: <incident capture>
```

## Constraints

- Prefer clear pass/fail checks over subjective validation.
- Keep deployment and verification ownership explicit.
- Record post-deploy findings for future release hardening.
- Always specify buildCommand and startCommand for production services.
- Document health check path and cold start behavior for free-tier services.
