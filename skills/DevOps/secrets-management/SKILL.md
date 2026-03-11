---
id: secrets-management
name: Secrets Management
description: Manage secrets securely across environments with rotation strategy, access controls, and leakage prevention practices.
category: DevOps
requires: []
examples:
  - Create a secrets management plan for this service across environments.
  - Review our secret rotation and access control workflow for risks.
---

# Secrets Management

Design and audit secrets workflows to minimize exposure and operational risk.

## When to Use

- You need to store, rotate, or audit sensitive credentials.
- You want to prevent secrets from leaking into code or logs.
- You need clear ownership and rotation procedures.

## Workflow

1. Inventory secrets by system and environment.
2. Classify access scope and ownership for each secret.
3. Define storage source and retrieval path.
4. Set rotation cadence and emergency revocation steps.
5. Validate audit logging and leak detection coverage.

## Vault and Provider Patterns

**HashiCorp Vault**: Use KV v2 engine with paths like `secret/data/<app>/<env>/<key>`. Fetch at runtime via `vault kv get` or the Vault API. Use short-lived tokens; avoid root tokens in application code.

**AWS Secrets Manager**: Store secrets by name, e.g. `prod/myapp/db-credentials`. Use IAM roles for retrieval; avoid long-lived access keys. Enable automatic rotation for RDS and similar integrations.

**GCP Secret Manager**: Path format `projects/<project>/secrets/<name>/versions/latest`. Use Workload Identity or service account keys (prefer Workload Identity). Grant `secretmanager.secretAccessor` only to the minimal set of identities.

**1Password CLI**: Use `op read "op://vault/item/field"` in CI or startup scripts. Integrate with `op run --env-file=.env` to inject secrets without writing them to disk. Use 1Password Service Accounts for automation.

## Common Pitfalls

- **Logging secret values**: Accidentally `console.log(config)` or including secrets in error messages. Fix: redact secrets in log formatters; never log full config objects.
- **Hardcoding in CI env**: Storing API keys in GitHub Actions secrets or similar is fine; hardcoding them in workflow YAML or scripts is not. Fix: always reference secrets via variables, never inline.
- **No rotation plan**: Secrets never rotate; compromise goes undetected. Fix: define cadence (e.g., 90 days), automate where possible, and test rotation in staging.
- **Shared service accounts**: One broad account used by many services increases blast radius. Fix: per-service identities with minimal permissions.

## Leak Detection

- **git-secrets**: Pre-commit hook that blocks commits containing patterns (API keys, private keys). Run `git secrets --scan` on history.
- **trufflehog**: Scans repos and history for high-entropy strings and known secret patterns. Use in CI: `trufflehog git file://. --only-verified`.
- **gitleaks**: Configurable rule-based scanner. Add to CI: `gitleaks detect --source . --verbose`. Maintain a `.gitleaks.toml` for custom patterns.

## Output Format

```markdown
## Secret Inventory
- <secret_name>: <owner> (<env>)

## Storage and Retrieval
- Provider: <Vault|AWS SM|GCP SM|1Password|other>
- Path/name: <path>
- Retrieval method: <API|CLI|SDK>

## Access Policy
- Principle: least privilege
- Access path: <service/account>
- Per-secret identity: <yes|no>

## Rotation Plan
- Cadence: <interval>
- Emergency revoke: <steps>
- Rotation tested: <yes|no>

## Leak Detection
- Tools: <git-secrets|trufflehog|gitleaks>
- CI integration: <yes|no>
- Pre-commit hooks: <yes|no>

## Controls Checklist
- [ ] No plaintext secrets in repo
- [ ] No secrets in logs or error messages
- [ ] Access logs enabled
- [ ] Rotation tested
- [ ] Per-service identities where possible
```

## Constraints

- Do not expose secret values, tokens, or keys in examples or logs.
- Enforce least-privilege access with explicit ownership per secret.
- Prefer automated rotation and revocation workflows over manual steps.