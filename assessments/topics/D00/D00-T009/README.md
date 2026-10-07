# D00-T009 Assessment Package — CI/CD Mental Model

This package evaluates whether the learner can reason about CI/CD as a delivery and feedback system rather than as a pipeline tool or YAML file.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Delivery Scenario](applied-scenario.md)
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
- No critical misconception around CI/CD definitions, artifact identity, deployment vs release, retry/concurrency, deployment verification, rollback limits, credentials, or GitOps

## Critical Misconceptions

A learner should not leave this topic believing that:

- CI/CD means Jenkins or one specific tool
- passing tests guarantees production safety
- continuous delivery and continuous deployment are the same
- rebuilding separately per environment is equivalent to promoting the same artifact
- caches are release artifacts
- deployment and release are identical
- blind retries are harmless
- approvals automatically make delivery safe
- a successful deployment command proves the service is healthy
- rollback always works
- GitOps replaces CI
