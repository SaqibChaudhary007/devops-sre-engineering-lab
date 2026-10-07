# D00-T012 Assessment Package — Reliability Engineering Foundations

This package evaluates whether the learner can reason about reliability from the user journey through failure, detection, containment, recovery, and improvement.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Reliability Scenario](applied-scenario.md)
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
- No critical misconception around reliability vs availability, SLI/SLO/SLA, error budgets, redundancy/failure domains, backup vs recovery, RTO/RPO, graceful degradation, capacity headroom, or failover readiness

## Critical Misconceptions

A learner should not leave this topic believing that:

- reliability means 100% uptime
- availability and reliability are the same thing
- more replicas automatically mean more reliability
- a backup proves recoverability
- failover automation proves failover readiness
- RTO and RPO are the same
- SLI, SLO, and SLA are interchangeable
- monitoring alone makes a system reliable
- high resource utilization automatically means user impact
- all services should target the same reliability
- redundancy helps even when all copies share the same failure domain
- every failure should be prevented instead of detected, contained, and recovered
