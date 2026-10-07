# D00-T017 Visual / Diagram Package — Systems Thinking

This package provides reusable diagrams for **00.17 — Systems Thinking**.

## Diagram Set

1. [DIA-D00-095 — System Boundary → Components → Relationships → Flows → Outcome](DIA-D00-095-system-boundary-components-flows-outcome.md)
2. [DIA-D00-096 — Stock / Flow / Queue Accumulation](DIA-D00-096-stock-flow-queue-accumulation.md)
3. [DIA-D00-097 — Reinforcing vs Balancing Feedback Loops](DIA-D00-097-reinforcing-vs-balancing-feedback.md)
4. [DIA-D00-098 — Local Optimization vs Global Outcome](DIA-D00-098-local-vs-global-optimization.md)
5. [DIA-D00-099 — Dependency Chain → Cascading Failure → Blast Radius](DIA-D00-099-dependency-cascade-blast-radius.md)
6. [DIA-D00-100 — Intervention → First-Order Effect → Second-Order Effect → New System State](DIA-D00-100-intervention-second-order-effects.md)

## Learning Progression

~~~text
System Boundary
→ Components
→ Relationships
→ Flows
→ Constraints
→ Feedback
→ Delays
→ Behavior Over Time
→ Intervention
→ New Behavior
~~~

## Design Rules

- stay provider-neutral
- reason about interactions and end-to-end outcomes rather than isolated component health
- show boundaries as chosen for the question being analyzed
- distinguish stock/accumulation from flow/rate
- show feedback loops as either reinforcing or balancing
- make delays visible because delayed feedback can destabilize control
- show bottleneck migration and local-vs-global optimization
- show hidden coupling and shared/common failure domains
- treat retries, autoscaling, alerts, automation, and humans as feedback mechanisms
- show architecture changes as interventions with possible second-order effects
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Formal system-dynamics equations, queueing theory, graph analysis, advanced control theory, causal inference, organizational-system modeling, and quantitative resilience modeling belong to later domains.
