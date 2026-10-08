# D00-T018 Assessment Package — Failure Thinking

This package evaluates whether the learner can reason about failure as a normal system condition and design detection, containment, recovery, and validation around realistic failure modes.

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
- No critical misconception around failure modes, retry amplification, common-mode failure, failover assumptions, backup vs recovery, RTO/RPO, or safe failure testing

## Critical Misconceptions

A learner should not leave this topic believing that:

- failure only means complete outage
- retries are always safe
- replicas automatically create resilience
- failover is guaranteed to work
- a successful backup proves recoverability
- every incident has exactly one isolated root cause
- slow, stale, partial, or incorrect behavior is not failure
- chaos engineering means random destruction
- a green health check alone proves recovery
- human/process/observability failures are outside the resilience model
