# D00-T017 Assessment Package — Systems Thinking

This package evaluates whether the learner can reason about systems as interacting wholes rather than as isolated components.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Systems Scenario](applied-scenario.md)
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
- No critical misconception around system boundaries, local-vs-global optimization, feedback loops, delays, retries as feedback, bottleneck migration, redundancy/common-mode failure, cascading failure, or second-order effects

## Critical Misconceptions

A learner should not leave this topic believing that:

- a system is just a list of components
- every problem has one isolated root cause
- healthy components guarantee a healthy system
- local optimization always improves the global outcome
- more capacity always solves performance problems
- retries are only local client behavior
- autoscaling reacts instantly
- redundancy automatically means independence
- queues are healthy if depth is stable
- humans and organizational incentives are outside the technical system
- architecture changes have only first-order effects
