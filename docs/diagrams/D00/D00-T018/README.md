# D00-T018 Visual / Diagram Package — Failure Thinking

This package provides reusable diagrams for **00.18 — Failure Thinking**.

## Diagram Set

1. [DIA-D00-101 — Fault → Error → Failure → Impact → Detection → Recovery](DIA-D00-101-fault-error-failure-impact-recovery.md)
2. [DIA-D00-102 — Failure Modes: Down / Slow / Stale / Wrong / Partial / Intermittent](DIA-D00-102-failure-modes-spectrum.md)
3. [DIA-D00-103 — Dependency Failure → Retry → Saturation → Cascading Failure](DIA-D00-103-retry-amplification-cascade.md)
4. [DIA-D00-104 — Failure Domain → Redundancy → Common-Mode Failure → Blast Radius](DIA-D00-104-failure-domain-redundancy-common-mode.md)
5. [DIA-D00-105 — Detect → Contain → Recover → Validate → Learn](DIA-D00-105-detect-contain-recover-validate-learn.md)
6. [DIA-D00-106 — Hypothesis → Controlled Failure Test → Observe → Stop → Recover → Learn](DIA-D00-106-controlled-failure-test-loop.md)

## Learning Progression

~~~text
Assumption
→ Fault / Stressor
→ Error / Degraded State
→ Failure Mode
→ User / System Impact
→ Detection
→ Containment
→ Recovery
→ Validation
→ Learning
~~~

## Design Rules

- stay provider-neutral
- treat complete outage as only one failure mode
- make slow, stale, incorrect, partial, intermittent and ambiguous behavior visible
- distinguish redundancy from true independence
- show retries as a possible amplifier, not an automatic fix
- show containment before perfect explanation when user impact is active
- make recovery validation explicit
- keep failure testing hypothesis-driven, bounded, observable, recoverable and authorized
- do not imply that chaos engineering means random destruction
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 foundation mental models only. Deep protocol behavior, quantitative reliability modeling, chaos tooling, distributed consensus internals, disaster-recovery implementation and production fault injection belong to later domains.
