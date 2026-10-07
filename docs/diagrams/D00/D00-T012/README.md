# D00-T012 Visual / Diagram Package — Reliability Engineering Foundations

This package provides reusable diagrams for **00.12 — Reliability Engineering Foundations**.

## Diagram Set

1. [DIA-D00-065 — Reliability vs Availability vs Durability vs Resilience](DIA-D00-065-reliability-availability-durability-resilience.md)
2. [DIA-D00-066 — User Journey → Dependency Chain → Reliability Outcome](DIA-D00-066-user-journey-dependency-reliability.md)
3. [DIA-D00-067 — Failure Domain → Blast Radius → Redundancy Placement](DIA-D00-067-failure-domain-blast-radius-redundancy.md)
4. [DIA-D00-068 — Detect → Contain → Recover → Validate → Learn](DIA-D00-068-detect-contain-recover-validate-learn.md)
5. [DIA-D00-069 — SLI → SLO → Error Budget Mental Model](DIA-D00-069-sli-slo-error-budget.md)
6. [DIA-D00-070 — Capacity Headroom → Failure → Failover / Degradation](DIA-D00-070-capacity-headroom-failure-recovery.md)

## Learning Progression

~~~text
User Journey
→ Reliability Target
→ Failure Model
→ Failure Domain
→ Detect
→ Contain
→ Recover
→ Validate
→ Learn
→ Improve
~~~

## Design Rules

- stay provider-neutral
- anchor reliability to important user journeys
- distinguish availability, durability, resilience, and recoverability
- show redundancy only in relation to independent failure domains
- show recovery as a sequence, not a magical event
- separate measured behavior (SLI), target (SLO), and allowed unreliability (error budget)
- show that recovery needs capacity headroom
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Detailed SLO engineering, burn rates, incident command, multi-region DR, chaos engineering, quantitative capacity planning, and platform-specific failover belong to later domains.
