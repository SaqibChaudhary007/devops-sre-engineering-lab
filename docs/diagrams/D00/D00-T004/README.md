# D00-T004 Visual / Diagram Package — Application Architecture Fundamentals

This package provides reusable diagrams for **00.04 — Application Architecture Fundamentals**.

## Diagram Set

1. [DIA-D00-017 — Client → Server → Data](DIA-D00-017-client-server-data.md)
2. [DIA-D00-018 — Three-Tier Architecture](DIA-D00-018-three-tier-architecture.md)
3. [DIA-D00-019 — Monolith vs Microservices](DIA-D00-019-monolith-vs-microservices.md)
4. [DIA-D00-020 — Synchronous vs Asynchronous Communication](DIA-D00-020-sync-vs-async.md)
5. [DIA-D00-021 — Stateful vs Stateless Scaling](DIA-D00-021-stateful-vs-stateless.md)
6. [DIA-D00-022 — Request Path & Failure Propagation](DIA-D00-022-request-path-failure-propagation.md)

## Learning Progression

~~~text
Client / Server
      ↓
Application Tiers
      ↓
Deployment Boundaries
      ↓
Communication Style
      ↓
State Placement
      ↓
Request Path
      ↓
Failure Propagation
~~~

## Design Rules

- one primary architecture idea per diagram
- simple learner-facing path first
- production/SRE implications where useful
- trade-offs instead of technology worship
- Mermaid source kept editable and reusable
- diagrams align with the canonical topic terminology

## Status

These diagrams are conceptual. Detailed protocol, networking, distributed-systems and persistence internals are intentionally deferred to later domains.
