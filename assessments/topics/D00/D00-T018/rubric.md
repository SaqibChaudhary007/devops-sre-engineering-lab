# D00-T018 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- failure is more than complete outage
- fault/error/failure are conceptually related but terminology varies
- failure mode describes how failure appears
- impact connects failure to users/business/system behavior
- partial/slow/stale/intermittent behavior can matter
- failure domains define correlated scope
- blast radius should be bounded
- common-mode dependencies can defeat redundancy
- overload and resource exhaustion can cascade
- retries can amplify failure
- timeout budgets bound waiting
- load shedding and backpressure protect constrained systems
- graceful degradation preserves critical capability
- circuit breakers are conditional patterns
- failover can fail
- backup existence does not prove recovery
- RTO and RPO are different business-driven objectives
- partition/quorum behavior is protocol-specific
- unknown outcomes require reconciliation
- changes, configuration, humans, observability, alerting, and runbooks can all contribute to failure
- containment can precede perfect explanation
- recovery must be validated end-to-end
- failure testing must be hypothesis-driven, bounded, observable, recoverable, and authorized
- chaos engineering is not random destruction

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T018

Critical misconception override: no competency if the learner believes retries always improve reliability, redundancy guarantees independence, failover cannot fail, backup success proves recovery, green component health proves healthy users, or chaos engineering means uncontrolled production disruption.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Fault / error / failure / impact classification | 10 |
| Failure modes / transient vs persistent reasoning | 10 |
| Failure domains / blast radius / common-mode risk | 15 |
| Timeout / retry amplification reasoning | 15 |
| Backpressure / shedding / graceful degradation | 10 |
| Failover assumptions / redundancy-vs-independence | 10 |
| Backup / restore / RTO / RPO reasoning | 10 |
| State uncertainty / duplicate-risk reasoning | 5 |
| Containment / recovery / validation | 10 |
| Safe failure-testing / pre-mortem / game-day design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- classify failure modes rather than use only up/down language
- identify user-visible impact
- map shared/common-mode failure domains
- show how slow dependencies can amplify retry and resource pressure
- compose timeout reasoning across layers
- treat retries as bounded policy
- use backpressure/load shedding/graceful degradation intentionally
- distinguish redundancy from independence
- test failover assumptions rather than trust topology diagrams
- distinguish backup creation from successful restore
- treat RTO/RPO as business-driven recovery objectives
- reconcile unknown outcomes rather than retry blindly
- contain impact before pursuing perfect explanation
- validate recovery using user/system/data/security evidence
- design failure testing with explicit stop conditions and authorization

## Follow-Up Evaluation

- L1: defines failure concepts
- L2: connects failure modes, dependencies, retries, and recovery
- L3: reasons through production propagation and mitigation
- L4: applies SRE thinking to overload, recovery, validation, and testing
- L5: designs failure domains, recovery topology, and resilience trade-offs

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

- fault/error/failure/failure mode → revisit sections 3–6 and OBS-D00-022
- failure types / gray / slow / stale → revisit sections 9–16 and OBS-D00-022
- failure domains / common mode / blast radius → revisit sections 7–8 and 19–21 plus OBS-D00-022
- overload / resource exhaustion / cascade → revisit sections 22–26 and EXP-D00-031
- timeout / retries / backoff / jitter → revisit sections 27–30 and EXP-D00-031
- shedding / backpressure / degradation → revisit sections 31–34 and EXP-D00-031
- isolation / circuit breaker / redundancy → revisit sections 35–39
- failover / failback / active-active/passive → revisit sections 38–41 and EXP-D00-032
- data failure / backup / restore / RTO / RPO → revisit sections 42–45 and EXP-D00-032
- partition / split-brain / quorum / state uncertainty → revisit sections 46–50 and EXP-D00-032
- change / config / security / human / observability failures → revisit sections 51–58
- detection / containment / recovery / validation / learning → revisit sections 59–63
- pre-mortems / failure testing / chaos / game days → revisit sections 64–70 and EXP-D00-032
- Senior/SRE/Architect reasoning → revisit sections 73–75
