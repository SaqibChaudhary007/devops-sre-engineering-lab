# D00-T004 Assessment Package — Application Architecture Fundamentals

This package evaluates whether the learner can reason about application components, request paths, state, dependencies, scaling and failure propagation.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Architecture Scenario](applied-scenario.md)
3. [Senior / SRE / Architect Follow-Ups](interview-followups.md)
4. [Teach-Back Assessment](teach-back.md)
5. [Rubric & Remediation Guide](rubric.md)

## Recommended Order

Knowledge Check
→ Applied Scenario
→ Follow-Ups
→ Teach-Back
→ Rubric Review

## Topic Competency Guidance

Recommended minimum:

- Knowledge Check: 80%
- Applied Scenario: 75%
- Follow-Up Depth: FD-3
- Reasoning Level: at least L3
- Teach-Back: 4/5 average
- No critical misconception about microservices, statelessness, load balancing, dependency chains or failure propagation

## Critical Misconceptions

A learner should not leave this topic believing that:

- microservices are always better
- stateless means the whole system has no state
- a load balancer guarantees high availability
- scaling application instances always fixes performance
- an API is only a URL
- the component showing the symptom must be the root cause
- async messaging removes all failure modes
- caches are free performance with no consistency cost
