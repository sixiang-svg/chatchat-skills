---
id: prowler-compliance
name: Prowler Compliance
description: Plan and interpret cloud security compliance scans with Prowler, including remediation prioritization and follow-up tracking.
category: DevOps
requires: []
examples:
  - Help me run a Prowler compliance review and prioritize remediation tasks.
  - Convert these Prowler findings into a risk-ranked action plan.
---

# Prowler Compliance

Use Prowler findings to drive practical and prioritized compliance improvements.

## When to Use

- You need to assess cloud environment compliance posture.
- You need to prioritize remediation based on severity and exposure.
- You want a repeatable reporting and tracking process.

## Concrete Prowler Patterns

**Cloud and framework commands:**
- AWS: `prowler aws --profile <profile> --compliance cis_aws`
- Azure: `prowler azure --subscription-id <id> --compliance cis_azure`
- GCP: `prowler gcp --project-id <id> --compliance cis_gcp`

**Compliance frameworks:** Use `--compliance` with `cis_aws`, `pci_dss`, `hipaa`, `soc2`, or custom JSON. Combine with `--checks` to scope: `prowler aws --checks check123 check456`. For custom checks, define in a JSON file and reference via `--compliance <path>`.

**Scoping:** Always limit scope to avoid noise and cost. Use `--region`, `--excluded-regions`, `--resource-tag`, or `--checks` to target specific services (e.g., IAM, S3, EC2). Running without scope limits produces thousands of findings and obscures priorities.

## Finding Interpretation Guide

**Severity vs compliance impact:** Prowler severity (critical, high, medium, low, informational) reflects exploitability and blast radius. Compliance impact maps to control requirements (e.g., PCI-DSS 3.4, CIS 1.1). A high-severity finding may fail multiple controls; an informational finding may indicate systemic gaps (e.g., missing MFA on service accounts) that warrant policy changes.

**Control mapping:** Map each finding to its control ID and requirement text. Use this to prioritize by audit deadlines and to group fixes that satisfy multiple controls at once.

## Remediation Wave Planning

**Critical first:** Address critical and high findings before any medium/low work. Group by service for efficiency; fix all IAM findings in one pass, then S3, then EC2, etc. This reduces context switching and re-scans.

**Wave structure:** Wave 1 = critical + high by service; Wave 2 = medium by service; Wave 3 = low and informational with policy exceptions documented. Assign owners per wave and set target dates with explicit re-scan criteria.

## Common Pitfalls

- **Running without scope limits:** Unscoped runs produce unmanageable output and slow remediation. Define accounts, regions, and checks upfront.
- **Ignoring informational findings:** Informational findings often indicate systemic issues (e.g., untagged resources, deprecated APIs). Review for patterns before dismissing.
- **Treating compliance as one-time:** Compliance is continuous. Schedule recurring scans and track drift.
- **Not tracking remediation progress:** Maintain a register of findings, owners, status, and re-scan evidence. Without tracking, fixes get lost and re-audits fail.

## Workflow

1. Define scope (accounts, services, compliance baseline).
2. Run Prowler with appropriate cloud and framework flags; collect and categorize findings by severity and control area.
3. Identify high-risk misconfigurations requiring immediate action.
4. Group medium/low findings into manageable remediation waves by service.
5. Produce owner-assigned remediation and revalidation plan with re-scan criteria.

## Output Format

```markdown
## Compliance Snapshot
- Scope: <accounts/services/regions>
- Framework: <CIS/PCI-DSS/HIPAA/SOC2>
- Critical findings: <count>
- High findings: <count>
- Medium/Low/Informational: <counts>

## Control Mapping Summary
- Controls failed: <list of control IDs>
- Controls partially satisfied: <list with gaps>

## Priority Actions
1. <critical remediation action> - Owner: <name> - Control: <ID>
2. <high priority remediation action> - Owner: <name> - Control: <ID>

## Remediation Waves
- Wave 1 (critical/high): <service> - Target: <date>
- Wave 2 (medium): <service> - Target: <date>
- Wave 3 (low/info): <service> - Target: <date>

## Remediation Plan
- Owner: <team/person>
- Target date: <date>
- Verification: <re-scan command and pass criteria>
- Tracking: <link to register or ticket>
```

## Constraints

- Prioritize exploitability and blast radius over raw finding count.
- Keep remediation actions specific and owner-assigned.
- Include explicit re-scan criteria after fixes.
- Do not run unscoped scans; always limit by account, region, or checks.
- Track remediation progress in a register; do not treat compliance as one-time.
