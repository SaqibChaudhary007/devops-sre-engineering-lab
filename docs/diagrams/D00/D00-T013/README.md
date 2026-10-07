# D00-T013 Visual / Diagram Package — SRE Foundations

This package provides reusable diagrams for **00.13 — SRE Foundations**.

## Diagram Set

1. [DIA-D00-071 — User Journey → SLI → SLO → Error Budget → Decision](DIA-D00-071-user-journey-sli-slo-error-budget-decision.md)
2. [DIA-D00-072 — Page vs Ticket vs Dashboard](DIA-D00-072-page-ticket-dashboard.md)
3. [DIA-D00-073 — Incident: Detect → Mitigate → Recover → Learn](DIA-D00-073-incident-detect-mitigate-recover-learn.md)
4. [DIA-D00-074 — Toil → Automation → Engineering Capacity](DIA-D00-074-toil-automation-engineering-capacity.md)
5. [DIA-D00-075 — Error Budget → Change Velocity / Reliability Trade-Off](DIA-D00-075-error-budget-change-velocity-reliability.md)
6. [DIA-D00-076 — Production Readiness → Operate → Incident → Improvement](DIA-D00-076-production-readiness-operate-improve.md)

## Learning Progression

~~~text
User Need
→ Measure
→ Set Objective
→ Manage Risk
→ Operate
→ Detect
→ Mitigate
→ Recover
→ Learn
→ Improve
~~~

## Design Rules

- stay provider-neutral
- anchor SRE decisions to user-visible service behavior
- keep SLI, SLO, SLA, and error-budget concepts distinct
- show page/ticket/dashboard as urgency/actionability decisions, not mandatory tooling
- separate mitigation from permanent correction
- show toil reduction as engineering work, not blind automation
- show progressive change as risk reduction, not proof of correctness
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Detailed SLO construction, burn-rate alerting, incident command, toil programs, on-call design, capacity forecasting, automated remediation, and platform-specific SRE implementation belong to later domains.
