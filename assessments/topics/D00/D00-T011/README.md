# D00-T011 Assessment Package — Distributed Systems Foundations

This package evaluates whether the learner can reason about distributed systems through uncertainty, partial failure, retries, consistency, queues, failure domains, and recovery rather than memorizing slogans.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Distributed Systems Scenario](applied-scenario.md)
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
- No critical misconception around ambiguous timeouts, retry safety, idempotency, duplicate effects, CAP, exactly-once scope, failure domains, queue capacity, backpressure, or cascading failure

## Critical Misconceptions

A learner should not leave this topic believing that:

- a timeout proves the remote operation failed
- retries always improve reliability
- every layer should retry independently
- exactly-once business effect is guaranteed by the queue alone
- event ordering is globally guaranteed
- replica count alone guarantees availability
- CAP means choose any two forever
- missed heartbeat proves a node is permanently dead
- queues provide infinite downstream capacity
- eventual consistency means incorrect data
- leader election alone guarantees consistency
- circuit breakers repair a failing dependency
