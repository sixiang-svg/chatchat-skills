---
id: incident-runbook-templates
name: Incident Runbook Templates
description: Produce practical incident runbooks with clear detection, triage, mitigation, and recovery steps. Use when standardizing on-call response for recurring production issues.
category: DevOps
requires: []
examples:
  - Create a runbook template for API latency spikes with owner, SLO impact, and rollback steps.
  - Draft an on-call runbook for database connection exhaustion with triage commands and escalation criteria.
---

# Incident Runbook Templates

Create incident runbooks that responders can execute quickly under pressure with minimal ambiguity and clear ownership.

## When to Use

- You need standardized response playbooks for known failure modes.
- You want consistent handoffs between on-call engineers.
- You need audit-friendly incident procedures and postmortem inputs.

## Runbook Patterns for Common Failure Modes

### Database Connection Exhaustion

**Detection**: Connection pool metrics at limit, "too many connections" errors, connection timeout spikes. **Triage**: Check active connections per app instance, idle vs active ratio, long-running queries. **Mitigation**: Kill idle connections, scale pool size (if headroom), restart app instances to release stuck connections. **Stop criteria**: Do not exceed max_connections; verify no connection leak before scaling.

### Disk Full

**Detection**: Disk usage >90%, write failures, "no space left" errors. **Triage**: `df`, `du` by directory, identify largest consumers (logs, temp, cache). **Mitigation**: Rotate/compress/delete old logs, clear temp, expand volume if no safe deletion. **Stop criteria**: Do not delete without verifying file purpose; never delete active DB files or config.

### Certificate Expiry

**Detection**: TLS handshake failures, cert expiry alerts, "certificate has expired" in logs. **Triage**: Check cert validity dates, which services use the cert. **Mitigation**: Deploy renewed cert, restart services that load cert at startup. **Stop criteria**: Verify new cert is valid before deploying; have rollback cert ready.

### Memory Leak

**Detection**: Gradual RSS growth, OOM kills, swap thrashing. **Triage**: Memory trend over time, heap dumps if available, top consumers. **Mitigation**: Restart affected instances to reclaim memory; schedule rolling restarts if leak is slow. **Stop criteria**: Restart is mitigation, not fix; file follow-up for root cause.

### DNS Resolution Failure

**Detection**: Name resolution timeouts, "could not resolve host" errors. **Triage**: `nslookup`, `dig` from affected hosts; check DNS server health; verify network path. **Mitigation**: Failover to backup DNS, restart stub resolver, check firewall/DNS policy. **Stop criteria**: Do not change DNS config without verifying impact on other services.

## Runbook Testing Methodology

### Game Days

Schedule periodic drills where the team executes runbooks against a non-production or isolated environment. Simulate the failure (e.g., fill disk, exhaust connections). Time the response. Identify steps that fail, commands that are wrong, or missing context. Update runbooks from findings.

### Tabletop Exercises

Walk through the runbook verbally without executing. Discuss: What would you do at step X? Who do you escalate to? What if step Y fails? Surface ambiguities and missing escalation paths. Update runbooks and escalation docs.

Run both at least quarterly. New runbooks must be tested before going live.

## Template Structure

Use this section order:

1. **Purpose and scope**: affected systems, customer impact, severity band.
2. **Detection signals**: alerts, dashboards, log patterns.
3. **Triage checklist**: immediate verification steps and key commands (`kubectl`, SQL, service health checks).
4. **Mitigation actions**: safest first moves and fallback options.
5. **Escalation path**: who to page, when, and what context to include.
6. **Recovery validation**: how to confirm service health restored.
7. **Post-incident actions**: follow-up tickets, owners, deadlines.

## Common Pitfalls

- **Runbooks that assume tribal knowledge**: Steps like "run the usual fix" or "check the dashboard" without URLs or exact commands. Every step must be executable by someone new to the system.
- **Untested commands**: Commands that are outdated, wrong for the environment, or have side effects. Test every command in a safe environment before publishing.
- **Missing escalation timeouts**: No "if not resolved in X minutes, escalate" criteria. Define timeouts (e.g., 15 min for SEV1) and escalation contacts.
- **No stop criteria**: Risky actions without "do not proceed if" conditions. Define when to halt (e.g., "do not scale if CPU is already saturated and cause is unknown").

## Output Format

```markdown
# Runbook: <incident type>

## Purpose and Scope
- Affected systems: <list>
- Customer impact: <description>
- Severity band: <SEV1-4>

## Trigger Conditions
- <alert or symptom>
- <dashboard/metric>

## Initial Triage (first 10 minutes)
- [ ] <step 1 with exact command>
- [ ] <step 2 with exact command>
- [ ] <verification: expected output>

## Mitigation
- Primary: <action with commands>
- Fallback: <action>
- Stop criteria: <do not proceed if...>

## Escalation
- Page: <team/role>
- Escalate when: <criteria>
- Timeout: <minutes before escalate>
- Context to include: <what to paste/send>

## Recovery Verification
- [ ] <metric check>
- [ ] <customer-impact check>
- [ ] <log pattern to confirm resolution>

## Post-Incident
- Follow-up ticket: <template>
- Owner: <role>
- Deadline: <e.g., within 24h>
```

## Constraints

- Keep every step executable and role-specific.
- Avoid runbooks that require tribal knowledge to interpret.
- Include rollback and stop conditions for risky mitigations.
- Include explicit "do not proceed" criteria when blast radius is unclear.