---
id: add-cdn-bundle
name: Add Cdn Bundle
description: Add a frontend build bundle to a CDN with versioning, cache strategy, integrity checks, and safe rollout guidance.
category: Development
requires: ["build artifact path", "cdn destination path"]
examples:
  - "Add this web bundle to our CDN with immutable hashed assets and a rollback path."
  - "Prepare a CDN deployment plan for this build output and verify cache headers."
---

# Add Cdn Bundle

Use this skill when shipping static frontend assets to a CDN.

## When to Use

- You are deploying JS/CSS/image assets to a CDN.
- You need cache-safe rollout and quick rollback.
- You want to avoid stale assets and broken references.

## Workflow

1. Build production assets with content hashing enabled.
2. Verify output manifest and entrypoints.
3. Upload assets to versioned prefix/path.
4. Apply cache headers:
   - hashed assets: long-lived immutable cache
   - HTML/manifest: short cache
5. Validate SRI/integrity and MIME types.
6. Perform canary or staged traffic rollout.
7. Confirm monitoring for 404/5xx and asset error rates.
8. Keep previous bundle path for rollback.

## Common Pitfalls

- Non-hashed filenames causing stale client bundles
- Caching HTML too aggressively
- Missing invalidation for non-versioned paths
- Mismatch between asset manifest and deployed files

## Output

- Deployment checklist and target paths
- Cache-control policy recommendation
- Rollout + rollback procedure
