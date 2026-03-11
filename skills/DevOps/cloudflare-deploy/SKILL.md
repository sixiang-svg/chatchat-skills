---
id: cloudflare-deploy
name: Cloudflare Deploy
description: Deploy applications to Cloudflare environments with pre-deploy checks, edge configuration validation, and rollback readiness.
category: DevOps
requires: []
examples:
  - Prepare a safe Cloudflare deployment checklist for this project.
  - Create a Cloudflare release plan with verification and rollback criteria.
---

# Cloudflare Deploy

Execute Cloudflare deployments with predictable verification and controlled rollback.

## When to Use

- You are deploying or updating workloads on Cloudflare.
- You need a repeatable release process for edge or serverless services.
- You want post-deploy validation tied to user-facing behavior.

## Workflow

1. **Confirm deployment target, environment, and release scope.** Distinguish Workers (serverless functions at the edge) from Pages (static or full-stack sites). Workers use `wrangler deploy`; Pages use `wrangler pages deploy` or Git integration. Verify `wrangler.toml` has `compatibility_date` set; missing it causes runtime errors.

2. **Validate configuration inputs and secrets.** Check KV, R2, D1, and other bindings in `wrangler.toml` match deployed resources. Run `wrangler kv:namespace list`, `wrangler r2 bucket list`, `wrangler d1 list` to confirm bindings exist. Validate secrets with `wrangler secret list` (values are hidden; ensure keys exist).

3. **Run pre-deploy checks and expected-behavior smoke tests.** Use `wrangler dev` locally to test bindings and routes. Run `wrangler deploy --dry-run --outdir=dist` to validate build without deploying. Verify route patterns (e.g., `example.com/*`) do not conflict with existing routes.

4. **Deploy with staged verification checkpoints.** Deploy to a staging or preview environment first. Use `wrangler tail` for live debugging during verification. Confirm routes in Cloudflare dashboard: Workers & Pages -> your worker -> Settings -> Triggers. Check that the deployed script matches the expected version.

5. **Trigger rollback when failure thresholds are reached.** Use version rollback (Workers: Versions tab), route revert, or cache purge as needed. Document thresholds (e.g., error rate > 5%, latency p99 > 2s).

## Common Pitfalls

- **Stale DNS cache after route changes.** Route updates can take minutes to propagate. Avoid assuming immediate effect; verify in dashboard and with `curl` from multiple locations.
- **Missing compatibility_date in wrangler.toml.** Workers require `compatibility_date` for runtime behavior. Deploying without it can cause undefined behavior or failures.
- **Deploying without testing bindings.** KV/R2/D1 bindings must exist before deploy. A typo in a binding name fails at runtime, not at deploy.
- **Forgetting to purge CDN cache.** After static asset or Worker response changes, purge cache via dashboard (Caching -> Configuration -> Purge Everything) or API to avoid serving stale content.

## Wrangler Commands and Dashboard Verification

**Deploy:**
```bash
wrangler deploy                    # Workers
wrangler pages deploy dist        # Pages (static)
wrangler deploy --env staging     # Environment-specific
```

**Validation and debugging:**
```bash
wrangler dev                      # Local dev with bindings
wrangler tail                    # Live log stream
wrangler kv:namespace list
wrangler r2 bucket list
wrangler d1 list
wrangler secret list
```

**Dashboard verification:** Workers & Pages -> select service -> Triggers (routes), Settings (bindings), Metrics (requests/errors). Caching -> Purge Everything when needed.

## Rollback Strategy

- **Version rollback (Workers):** Dashboard -> Workers & Pages -> your worker -> Versions -> select previous version -> Deploy. Restores prior script without code change.
- **Route revert:** Remove or adjust route in Triggers to point to previous worker or disable. Use when route config is wrong.
- **Cache purge:** Caching -> Purge Everything (or Purge by URL). Use when static assets or cached responses are stale; does not revert Worker code.

## Output Format

```markdown
## Release Scope
- Service: <name>
- Type: Workers | Pages
- Environment: <target>

## Pre-Deploy Checks
- [ ] wrangler.toml validated (compatibility_date, bindings)
- [ ] KV/R2/D1 bindings exist and match config
- [ ] Secrets validated
- [ ] Local smoke test (wrangler dev) pass
- [ ] Route patterns verified (no conflicts)

## Deploy
- Command: <wrangler deploy or pages deploy>
- [ ] Staging/preview deployed first

## Verification
- [ ] Critical route check (curl from edge)
- [ ] wrangler tail shows expected behavior
- [ ] Dashboard: Triggers, bindings, metrics
- [ ] Error rate and latency within threshold

## Rollback
- Trigger: <condition, e.g., error rate > 5%>
- Action: <version rollback | route revert | cache purge>
- [ ] Rollback steps documented and tested
```

## Constraints

- Do not skip environment-specific validation.
- Keep rollback criteria objective and measurable.
- Document assumptions around DNS, caching, and edge behavior.
- Always set compatibility_date in wrangler.toml.
- Validate bindings before deploy; test with wrangler dev.
- Purge cache when static or cached content changes.