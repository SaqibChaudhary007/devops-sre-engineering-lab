# D00-T016 Assessment Package — Automation Mental Models

This package evaluates whether the learner can reason about automation as a bounded, state-aware, observable operating capability rather than simply scripting repetitive tasks.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Automation Scenario](applied-scenario.md)
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
- No critical misconception around idempotency, retries, state, reconciliation, validation, partial failure, human approval boundaries, automation identity, blast radius, or bounded remediation

## Critical Misconceptions

A learner should not leave this topic believing that:

- automation means scripting everything
- every repetitive task should be automated
- successful process execution proves successful outcome
- retries are always safe
- idempotency means guaranteed success
- rollback is always possible
- duplicate execution can be ignored
- self-healing means retry/restart forever
- human approval means automation failed
- admin permissions make automation safer
- automation does not need observability or auditability
- AI-generated actions should be fully autonomous by default
