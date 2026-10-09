# D00-T018 Assessment Package — Failure Thinking

This package evaluates whether the learner can reason about failure as a normal system condition: identify failure modes, understand propagation, limit blast radius, recover safely, and validate resilience.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Failure Scenario](applied-scenario.md)
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
- No critical misconception around failure modes, retry amplification, common-mode failure, failover assumptions, backup-vs-recovery, recovery validation, or chaos/failure-testing safety

## Critical Misconceptions

A learner should not leave this topic believing that:

- failure only means complete outage
- every incident has one isolated root cause
- retries always improve reliability
- replicas automatically mean resilience
- failover is guaranteed to work
- a successful backup means recovery is proven
- green health checks prove users are healthy
- stale or incorrect data is always acceptable if the service is available
- chaos engineering means randomly breaking production
- recovery is complete when one metric becomes green
