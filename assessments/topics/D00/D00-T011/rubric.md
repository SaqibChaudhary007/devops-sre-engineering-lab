# D00-T011 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- distributed systems combine network communication with independent failure
- partial failure is normal
- timeout means uncertainty, not proof of non-execution
- retries can recover transient faults or amplify overload
- idempotency/request identity control duplicate side effects
- retry ownership and retry budgets should be explicit
- backoff and jitter solve different retry-pressure problems
- circuit breakers and bulkheads contain failure rather than repair dependencies
- at-least-once delivery can produce duplicates
- exactly-once guarantees are scoped; business effect remains end-to-end
- ordering guarantees are scoped
- replication introduces lag and stale-read questions
- consistency requirements depend on business correctness
- CAP is a partition-time consistency-versus-availability trade-off
- failure detection is inferred
- replica count must be evaluated against failure domains
- queues buffer and decouple but do not provide infinite capacity
- backpressure protects downstream capacity
- hot partitions can be hidden by averages
- graceful degradation can preserve critical user flows
- distributed observability requires correlation across services

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T011

Critical misconception override: no competency if the learner believes timeout proves failure, retries are always safe, exactly-once transport guarantees one business effect, CAP means choose any two forever, replicas automatically guarantee availability, missed heartbeat proves permanent failure, or queues provide unlimited capacity.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Distributed path / partial-failure reasoning | 10 |
| Ambiguous timeout / idempotency | 15 |
| Retry amplification / ownership / resilience controls | 15 |
| Replication lag / consistency | 10 |
| CAP / partition reasoning | 10 |
| Failure-domain reasoning | 10 |
| Queue backlog / backpressure | 10 |
| Duplicate delivery / hot-tenant handling | 5 |
| Graceful degradation / observability | 5 |
| Senior / SRE / Architect target design | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- separate caller observation from remote reality
- preserve one logical request identity across retries
- prevent duplicate payment effects
- avoid retries at every layer
- bound retries and use backoff/jitter
- use circuit breaker behavior carefully
- connect replica lag to business correctness
- explain CAP under partition rather than as a permanent slogan
- spread replicas across meaningful failure domains
- recognize sustained queue overload
- design backpressure and admission control
- detect hot tenants/partitions with granular metrics
- handle at-least-once duplicate delivery
- degrade noncritical functionality safely
- correlate evidence across services

## Follow-Up Evaluation

- L1: defines distributed-systems concepts
- L2: connects timeouts, retries, replication, queues, and failure domains
- L3: diagnoses ambiguous and cascading failures
- L4: connects system behavior to SLO/recovery outcomes
- L5: designs distributed correctness and resilience trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware, and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- distributed foundations / partial failure → revisit sections 3–7 and OBS-D00-015
- latency / timeout reasoning → revisit sections 8–11 and OBS-D00-015
- retries / idempotency / duplicate work → revisit sections 12–17 and EXP-D00-017
- ordering / time / causality → revisit sections 18–20
- replication / consistency / stale reads → revisit sections 21–28 and EXP-D00-018
- partitions / CAP / failure detection → revisit sections 29–38 and EXP-D00-018
- backoff / jitter / resilience controls → revisit sections 39–43 and EXP-D00-017
- queues / backpressure → revisit sections 44–46 and EXP-D00-018
- sharding / caching / transactions → revisit sections 47–53
- cascading failure / blast radius → revisit sections 54–59
- observability → revisit sections 60–63
- Senior/SRE/Architect reasoning → revisit sections 69–71
