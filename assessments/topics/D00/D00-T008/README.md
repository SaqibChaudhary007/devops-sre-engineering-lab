# D00-T008 Assessment Package — Infrastructure as Code Mental Model

This package evaluates whether the learner can reason about Infrastructure as Code as an operating model for controlled infrastructure change rather than as a single tool.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied IaC Change Scenario](applied-scenario.md)
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
- No critical misconception around state, drift, plan/apply, replacement risk, locking, import, rollback, or GitOps

## Critical Misconceptions

A learner should not leave this topic believing that:

- IaC means Terraform only
- all IaC tools require a state file
- remote state always guarantees locking
- declarative automatically means safe
- plan/preview guarantees successful execution
- reverting Git automatically rolls infrastructure back
- import reconstructs original design intent
- idempotence is universal across all tools/modules
- GitOps and IaC are the same thing
- a syntactically valid plan is operationally safe
