# D00-T005 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- physical infrastructure underpins virtual infrastructure
- host and guest are distinct layers
- vCPU is an abstraction and not always a dedicated physical core
- storage access models differ between block, file, and object
- persistence guarantees must be proven, not assumed
- guest-visible devices do not prove physical topology
- routing controls network reachability
- failure domains are shared dependencies that can fail together
- redundancy only helps when it spans meaningful failure domains
- high availability requires failover, capacity, state, and dependency design
- utilization is not the same as saturation
- headroom matters during spikes and failures
- IaC improves repeatability and review but not automatic correctness
- cloud does not eliminate failure, capacity, security, or cost concerns

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T005

Critical misconception override: no competency if the learner believes one vCPU always equals one physical core, two VMs automatically mean HA, low CPU proves infrastructure health, or IaC/cloud remove infrastructure failure risk.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Impact & assumption challenge | 10 |
| Failure-domain reasoning | 15 |
| Infrastructure dependency path | 15 |
| Storage reasoning | 10 |
| Capacity/headroom reasoning | 10 |
| Evidence selection | 10 |
| Senior troubleshooting sequence | 10 |
| SRE/reliability reasoning | 10 |
| Architecture/IaC trade-offs | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- reject CPU-only diagnosis
- identify shared host/failure-domain risk
- distinguish guest evidence from physical topology assumptions
- treat storage and network as possible shared dependencies
- reason about failover headroom beyond CPU
- ask for placement and persistence evidence
- separate mitigation from long-term resilience design
- use IaC for traceability/repeatability without assuming it guarantees correctness

## Follow-Up Evaluation

- L1: defines infrastructure components
- L2: connects physical, virtual, storage, and network layers
- L3: diagnoses failure domains, persistence, routing, and capacity issues
- L4: connects infrastructure behavior to SLOs and recovery
- L5: evaluates infrastructure trade-offs from requirements and constraints

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- physical/virtual infrastructure → revisit sections 3–10 and OBS-D00-008/009
- storage → revisit sections 11–16 and OBS-D00-008/009
- networking → revisit sections 17–22 and OBS-D00-008
- failure domains/zones/regions → revisit sections 23–26 and OBS-D00-009
- provisioning/mutable/immutable/IaC → revisit sections 27–32
- capacity/utilization/headroom → revisit sections 33–37 and EXP-D00-006
- redundancy/HA → revisit sections 38–40
- cloud/shared responsibility → revisit sections 41–42
- security/performance/cost → revisit sections 43–45
- Senior/SRE/Architect reasoning → revisit sections 46–50
