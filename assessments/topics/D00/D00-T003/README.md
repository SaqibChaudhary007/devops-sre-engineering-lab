# D00-T003 Assessment Package — Software Engineering Foundations

This package evaluates whether the learner can reason about the path from source code to a runnable production application.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Scenario](applied-scenario.md)
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
- No critical misconception about source, runtime, build, artifact, dependency or configuration

## Critical Misconceptions

A learner should not leave this topic believing that:

- source code and artifact are the same thing
- successful compilation guarantees successful runtime behavior
- runtime dependencies are only a developer concern
- configuration changes always require rebuilding the application
- a lockfile guarantees full reproducibility
- containers eliminate all environment differences
- the same source always produces the same result regardless of toolchain/environment
- CI/CD makes poor software design correct
