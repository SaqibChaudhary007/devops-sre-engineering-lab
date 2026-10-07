# D00-T010 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- containers isolate processes; they are not complete VMs
- image and container are separate lifecycle objects
- tags are weaker identity than immutable digests
- images have layers; running containers have writable runtime state
- local writable state should not be assumed durable
- runtime and host responsibilities are separate
- namespaces isolate views; cgroups govern resources
- resource request/limit semantics should not be overgeneralized
- startup, liveness, and readiness answer different questions
- restart is not root-cause recovery
- orchestration exists to manage desired workload state across hosts
- reconciliation is continuous control-loop behavior
- scheduling depends on capacity and constraints
- service discovery abstracts changing instance identities
- replica count alone does not guarantee availability
- stateful workloads require stronger identity/storage/recovery handling
- logs/metrics/events should survive ephemeral workload replacement
- Kubernetes is an orchestrator, not the container runtime
- self-healing is bounded by platform and dependency conditions

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T010

Critical misconception override: no competency if the learner believes container = VM, image = running container, local writable state is automatically durable, restart = root-cause recovery, probes are interchangeable, replicas guarantee availability, orchestration creates capacity, Kubernetes = runtime, or self-healing is unlimited.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Layer / image identity reasoning | 10 |
| Ephemeral vs persistent data | 10 |
| Health / restart-loop reasoning | 15 |
| Desired state / scheduling / capacity | 15 |
| Service discovery / network reasoning | 10 |
| Rolling-update reasoning | 10 |
| Stateful recovery reasoning | 10 |
| Observability / evidence design | 5 |
| Security boundary reasoning | 5 |
| Senior / SRE / Architect target design | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should:

- separate image/container/runtime/host/orchestrator layers
- require exact image identity for traceability
- move durable uploads outside writable container state
- separate startup/liveness/readiness/service health
- investigate restart loops rather than celebrate automatic restart
- recognize node-level blast radius
- explain why capacity can block reconciliation
- use stable service discovery instead of instance addresses
- recognize path-specific dependency failures
- stop/slow rollout when new replicas are not ready
- treat stateful recovery as identity/storage/consistency work
- centralize evidence for ephemeral workloads
- reject unlimited-self-healing assumptions

## Follow-Up Evaluation

- L1: defines image/container/orchestration concepts
- L2: connects runtime, host, health, storage, and scheduling
- L3: diagnoses layered container/orchestration failures
- L4: connects runtime behavior to reliability/recovery
- L5: designs platform, state, placement, capacity, and ownership boundaries

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

- container/image/runtime foundations → revisit sections 3–21 and OBS-D00-014
- resource governance → revisit sections 22–23
- networking/config/secrets → revisit sections 24–27
- health/restart → revisit sections 28–29 and EXP-D00-015
- orchestration/reconciliation → revisit sections 30–36
- scheduling/placement/service discovery → revisit sections 37–40 and EXP-D00-016
- scaling/updates → revisit sections 41–43
- stateless/stateful/storage → revisit sections 44–46
- failure/rescheduling → revisit sections 47–50
- observability/security → revisit sections 51–55
- CI/CD/IaC/Kubernetes boundaries → revisit sections 56–60
- Senior/SRE/Architect reasoning → revisit sections 61–65
