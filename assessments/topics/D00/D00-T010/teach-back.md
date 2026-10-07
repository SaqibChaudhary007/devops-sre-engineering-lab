# D00-T010 — Teach-Back Assessment

## Goal

Demonstrate that you can explain containers and orchestration without reducing them to Docker or Kubernetes commands.

## Task A — Beginner

Explain:

- what an image is
- what a container is
- why containers exist

Use one simple analogy.

## Task B — Engineer

Explain:

~~~text
Image
→ Runtime
→ Container
→ Host
~~~

Then explain what the host still provides.

## Task C — Container vs VM

Explain why:

~~~text
Container
≠
Small VM
~~~

Focus on kernel and isolation boundaries.

## Task D — State Challenge

Explain:

- image layers
- writable container layer
- ephemeral state
- persistent state
- why workload and storage lifecycle differ

## Task E — Health Challenge

Explain the difference between:

~~~text
Startup
Liveness
Readiness
Service Health
~~~

Then explain why using one signal for all four can be dangerous.

## Task F — Senior Engineer

Explain:

~~~text
Desired replicas = 4
Observed replicas = 3
~~~

Then explain reconciliation, scheduling, and the case where no suitable node exists.

## Task G — SRE

Explain how to reason about:

- container failure
- node failure
- replica health
- capacity
- service discovery
- SLO impact
- restart loops
- rollout failures

## Task H — Architect

Explain how you would design:

- image identity
- state placement
- failure-domain spread
- spare capacity
- service discovery
- health models
- persistent storage
- observability
- security boundaries

## Kubernetes Challenge

Explain why:

> "Kubernetes is the container runtime"

is incorrect.

Then explain how Kubernetes, node runtime, and containers relate.

## Self-Healing Challenge

Explain why:

> "Kubernetes self-heals everything"

is incorrect.

Include:

- capacity
- storage
- networking
- dependencies
- configuration
- control-plane health

## Scoring

Score 1–5 for:

- correctness
- clarity
- image/container/runtime/host reasoning
- state/persistence reasoning
- health/reconciliation reasoning
- reliability awareness
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.
