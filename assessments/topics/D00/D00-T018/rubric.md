# D00-T018 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- fault, internal degradation, failure, and impact are related but distinct
- failure mode describes how a workload fails
- failure can be slow, partial, stale, incorrect, intermittent, or unavailable
- failure domains define correlated scope
- blast radius should be bounded
- common-mode failure can defeat redundancy
- overload can create cascading failure
- retries can amplify failure
- timeouts and fail-fast behavior bound resource consumption
- backpressure and load shedding protect constrained systems
- graceful degradation preserves critical functionality
- circuit breakers are conditional patterns
- redundancy requires sufficient independence
- failover has assumptions and failure modes
- backup does not prove restore capability
- RTO and RPO are distinct recovery objectives
- partition/quorum behavior is protocol-specific
- state uncertainty creates duplicate-processing risk
- configuration, security controls, humans, observability, alerting, and runbooks can all participate in failure
- containment can precede full RCA
- recovery must be validated end-to-end
- pre-mortems, game days, and bounded failure testing improve resilience confidence
- chaos engineering is controlled experimentation, not random breakage

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T018

Critical misconception override: no competency if the learner believes failure only means complete outage, retries are always safe, replicas automatically guarantee resilience, failover is guaranteed, successful backup proves recoverability, one green health check proves recovery, or chaos engineering means random destruction.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Fault/error/failure/impact reasoning | 10 |
| Failure-mode classification | 10 |
| Failure domains / blast radius / common-mode risk | 10 |
| Timeout / retry / amplification reasoning | 15 |
| Backpressure / load shedding / degradation | 10 |
| Redundancy / failover readiness | 10 |
| Backup / restore / RTO / RPO | 10 |
| State uncertainty / duplicates / protocol-specific partition reasoning | 10 |
| Containment / recovery validation | 10 |
| Senior / SRE / Architect target design | 5 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- distinguish initiating stressor from user-visible failure
- classify slow/partial/gray behavior accurately
- identify shared/common-mode dependencies
- map likely blast radius without pretending certainty
- compose timeout and retry reasoning across layers
- show how retries amplify overload
- use backpressure/load shedding/graceful degradation appropriately
- reject replica count as proof of independence
- identify failover preconditions and gaps
- distinguish backup evidence from recovery evidence
- define RTO/RPO as business-driven objectives
- handle unknown outcomes with identity/reconciliation/idempotency
- keep partition/quorum reasoning protocol-specific
- prioritize containment during active impact
- validate recovery using user/system/data/security evidence
- design safe bounded tabletop/failure-testing scenarios

## Follow-Up Evaluation

- L1: defines failure concepts
- L2: connects failure modes, domains, propagation, and recovery
- L3: reasons through production failure and mitigation
- L4: applies SRE thinking to overload, containment, recovery confidence, and testing
- L5: designs resilience architecture and recovery trade-offs

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

- fault / error / failure / impact → revisit sections 3–6 and OBS-D00-022
- failure domains / blast radius / common-mode failure → revisit sections 7–8 and 19–21, plus OBS-D00-022
- transient / intermittent / partial / gray / slow failure → revisit sections 9–16 and OBS-D00-022
- dependency / cascading / overload failure → revisit sections 17–26 and EXP-D00-031
- timeout / fail-fast / retries / backoff / jitter → revisit sections 27–30 and EXP-D00-031
- load shedding / backpressure / degradation / isolation / circuit breaker → revisit sections 31–36 and EXP-D00-031
- redundancy / failover / failback → revisit sections 37–41 and EXP-D00-032
- data failure / backup / restore / RTO / RPO → revisit sections 42–45 and EXP-D00-032
- partition / split-brain / quorum / state uncertainty / duplicates → revisit sections 46–50 and EXP-D00-032
- change / config / security / human / observability / alert / runbook failure → revisit sections 51–58
- detection / containment / recovery / validation / learning → revisit sections 59–63
- pre-mortem / failure testing / chaos / game day → revisit sections 64–70 and EXP-D00-032
- Senior/SRE/Architect reasoning → revisit sections 73–75
