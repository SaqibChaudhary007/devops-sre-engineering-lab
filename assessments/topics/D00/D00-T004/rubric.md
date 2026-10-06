# D00-T004 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- client/server as interaction roles
- architecture as components, responsibilities, interfaces, communication and state
- three-tier architecture as responsibility separation
- monolith and microservices as trade-off choices
- API as contract, not only endpoint
- synchronous calls create direct waiting dependencies
- asynchronous messaging trades immediate coupling for queue/delivery complexity
- stateless instances improve replaceability but the system may still have state
- state placement affects scaling and failover
- databases, caches, queues and external systems are dependencies
- load balancing distributes traffic but does not guarantee availability
- horizontal scaling does not automatically fix shared bottlenecks
- dependency chains affect end-to-end latency
- failures can propagate or cascade

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T004

Critical misconception override: no competency if the learner believes microservices are always better, stateless means no state exists, load balancing guarantees HA, or app-tier scaling always removes bottlenecks.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Impact & scope | 10 |
| Request-path understanding | 10 |
| State reasoning | 15 |
| Dependency/bottleneck reasoning | 15 |
| Database reasoning | 10 |
| Evidence selection | 10 |
| Senior troubleshooting sequence | 10 |
| SRE/reliability reasoning | 10 |
| Architecture/trade-offs | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- identify more than one possible constraint
- explain why app-tier scaling alone may fail
- treat database and external dependency latency as hypotheses supported by evidence
- identify local session state as a separate architecture issue
- request end-to-end and dependency-level telemetry
- avoid jumping straight to microservices
- distinguish mitigation from permanent architecture changes

## Follow-Up Evaluation

- L1: defines architecture components
- L2: connects request paths and state
- L3: diagnoses dependencies, scaling and failure propagation
- L4: connects architecture behavior to SLOs and incident response
- L5: evaluates boundaries, availability and trade-offs from requirements

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- client/server/request path → revisit sections 3–7 and OBS-D00-007
- monolith/microservices → revisit sections 8–11
- API contracts → revisit sections 12–13
- sync/async → revisit sections 14–15 and EXP-D00-005
- state/statelessness → revisit sections 16–18 and EXP-D00-004
- database/cache/load balancer → revisit sections 19–23
- dependencies/failure propagation → revisit sections 24–35
- architecture trade-offs → revisit sections 37–41
