---
id: sast-configuration
name: SAST Configuration
description: Configure static application security testing in CI pipelines with policy thresholds, triage flow, and false-positive controls.
category: DevOps
requires: []
examples:
  - Set up SAST checks for pull requests with severity-based merge gates.
  - Review an existing SAST policy that blocks too many low-value findings.
---

# SAST Configuration

Design actionable SAST enforcement that improves security without blocking delivery.

## When to Use

- You need automated static code security checks in CI/CD.
- You need consistent triage criteria for vulnerabilities and false positives.
- You are tuning enforcement thresholds to balance risk and developer velocity.

## SAST Integration Patterns

**Semgrep:** Lightweight, fast; supports 30+ languages. Use `semgrep scan --config auto` for OSS rules, or `p/security-audit` for security-focused checks. Integrates via `semgrep ci` in GitHub Actions, GitLab CI, or generic CI. Output SARIF for unified reporting.

**CodeQL:** Deep semantic analysis; best for JavaScript/TypeScript, Python, Java, C#, Go, Ruby. Use `codeql database create` then `codeql database analyze`. Native GitHub Actions integration; supports custom queries in `.ql` files.

**SonarQube:** Full-featured platform with security, quality, and coverage. Run via SonarScanner in CI; supports branch analysis and PR decoration. Use Quality Gates to enforce severity thresholds and new-code metrics.

**Bandit (Python):** Python-specific; fast and low-false-positive for common issues (SQLi, hardcoded secrets, unsafe deserialization). Run `bandit -r . -f json`; integrate in pre-commit or CI. Combine with Semgrep or CodeQL for broader coverage.

## Baseline Management

**Differential scanning:** Only fail on new findings introduced in the current branch/PR. Establish baseline from main; compare against it. Prevents blocking on legacy debt while enforcing clean new code.

**Suppression with audit trail:** Every suppression must include: finding ID, justification, owner, and expiry date. Store in version-controlled config (e.g., `semgrep.yml` inline suppressions, CodeQL `codeql-config.yml`). Review suppressions quarterly.

**Baseline modes:** "New findings only" (recommended for adoption) vs "full scan" (for mature teams). Start with new-only; migrate to full scan once backlog is manageable.

## Rule Customization

**Custom rules:** Write org-specific rules for internal APIs, frameworks, or patterns. Semgrep uses YAML rules; CodeQL uses `.ql`; SonarQube uses rule templates. Target high-signal patterns (auth bypass, injection, secret exposure) before style or low-impact checks.

**Severity mapping:** Map tool severities to your policy. Not all tools use Critical/High/Medium/Low consistently. Define a canonical mapping and document it. Gate on your canonical severity, not raw tool output.

## CI Integration Patterns

**PR checks:** Run SAST on every PR; block merge when gate threshold is exceeded. Use `fail-on` or equivalent to control behavior. Ensure scans complete within PR SLA (e.g., &lt; 10 min).

**Scheduled full scans:** Run full baseline scans nightly or weekly; track trend and backlog. Use for reporting, not merge gates.

**Branch protection:** Require SAST check to pass before merge. Combine with required reviews to prevent bypass.

## Common Pitfalls

- **Blocking on all findings from day one:** Causes immediate friction and bypass. Use baseline or new-findings-only mode; phase in strict gates.
- **No baseline causing alert flood:** Hundreds of legacy findings overwhelm triage. Establish baseline, suppress or fix backlog, then enforce on new code.
- **Suppressing without justification:** Technical debt grows; real issues get buried. Require justification and expiry for every suppression.
- **Not tuning rules for language/framework:** Default rule sets include irrelevant checks. Disable low-signal rules; add custom rules for your stack.

## Workflow

1. Identify repositories, languages, and scan coverage requirements.
2. Select and configure SAST tool(s) for your stack.
3. Define severity thresholds and branch protection behavior.
4. Configure baseline handling (differential scanning, new vs full).
5. Establish triage ownership, SLA targets, and suppression rules with audit trail.
6. Validate scan reliability and signal quality in pull request flows.

## Output Format

```markdown
## SAST Policy
- Scope: <repos/languages>
- Tool(s): <Semgrep/CodeQL/SonarQube/Bandit/other>
- Gate threshold: <severity and count rules>
- Baseline mode: <new findings only / full scan / differential>

## CI Integration
- PR check: <command/config>
- Schedule: <frequency for full scan>
- Branch protection: <required checks>

## Rule Configuration
- Custom rules: <count, location>
- Severity mapping: <tool -> policy>
- Disabled rules: <list or reference>

## Triage Process
- Owner: <team/role>
- SLA: <time to triage>
- Suppression criteria: <allowed cases>
- Audit: <justification + expiry required>

## Enforcement Checklist
- [ ] PR checks run on target branches
- [ ] Baseline established and documented
- [ ] Severity policy and mapping documented
- [ ] Suppression process with audit trail defined
- [ ] False-positive process defined
```

## Constraints

- Prefer measurable, auditable policy rules over informal guidance.
- Require justification and expiry for suppressions where possible.
- Avoid vendor lock-in details unless the user requests a specific tool.