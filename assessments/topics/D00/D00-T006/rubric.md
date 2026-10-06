# D00-T006 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- cloud includes on-demand self-service, network access, pooling, elasticity, and metering
- cloud is API-driven and automation-friendly
- control plane and data plane are distinct concerns
- scalability and elasticity are related but different
- autoscaling depends on correct signals, architecture, quotas, and downstream capacity
- regions/zones are provider-specific failure-domain abstractions
- managed services shift responsibility rather than eliminate it
- IaaS/PaaS/SaaS/serverless differ in abstraction and responsibility
- public cloud does not mean publicly reachable
- private cloud is more than virtualization
- multi-cloud is industry terminology, not a formal NIST deployment model
- ephemeral compute should not hold irreplaceable state
- quotas/service limits constrain architecture
- metering connects architecture to cost
- governance enables safe self-service
- blast radius and resilience must be designed
- cloud-native is broader than Kubernetes

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T006

Critical misconception override: no competency if the learner believes managed services remove all customer responsibility, serverless means no servers, autoscaling guarantees performance, multi-zone equals DR, cloud has unlimited capacity, or cloud-native means Kubernetes.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Control/data-plane reasoning | 10 |
| Autoscaling/quota diagnosis | 15 |
| State-placement reasoning | 10 |
| Dependency-capacity reasoning | 15 |
| Failure-domain reasoning | 10 |
| Shared-responsibility reasoning | 10 |
| Cost/governance reasoning | 10 |
| Senior troubleshooting sequence | 10 |
| SRE / architecture trade-offs | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- separate management-path health from workload-path health
- identify the quota ceiling
- explain why moderate CPU does not prove health
- identify local session state as a scaling problem
- identify the managed database as a dependency bottleneck
- reason about one-zone blast radius
- separate provider responsibility from customer responsibility
- connect autoscaling to cost
- propose governance without blocking useful self-service
- avoid suggesting multi-cloud without a requirement

## Follow-Up Evaluation

- L1: defines cloud concepts
- L2: connects service models, control/data planes, scaling, and responsibility
- L3: diagnoses quota, state, dependency, and failure-domain issues
- L4: connects cloud abstractions to SLOs, recovery, and governance
- L5: evaluates provider abstractions and trade-offs from requirements

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

- cloud operating model → revisit sections 3–9 and OBS-D00-010
- scalability/elasticity/autoscaling → revisit sections 10–13 and EXP-D00-008
- regions/zones/failure domains → revisit sections 14–16 and EXP-D00-008
- managed services/service models → revisit sections 17–24 and EXP-D00-007
- public/private/hybrid/multi-cloud → revisit sections 25–28
- ephemeral/persistent/immutable → revisit sections 29–32
- identity/tags/quotas → revisit sections 33–37
- metering/cost/governance → revisit sections 38–43 and EXP-D00-008
- observability/blast radius/resilience → revisit sections 44–50
- Senior/SRE/Architect reasoning → revisit sections 51–55
