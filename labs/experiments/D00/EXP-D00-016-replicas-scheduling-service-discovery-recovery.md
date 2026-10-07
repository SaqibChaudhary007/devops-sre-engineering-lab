---
id: EXP-D00-016
domain: D00
topics:
  - D00-T010
level: L2-L3
type: experiment
status: draft
estimated_time: 55-75m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-016 — Desired Replicas, Scheduling, Service Discovery, and Failure Recovery

## Objective

Practice reasoning about desired state, scheduling, service discovery, load balancing, node failure, and self-healing boundaries.

## Safety

This is a local architecture exercise only.

No cluster, cloud account, or destructive command is required.

## Scenario

A web service is configured with:

~~~text
Desired replicas = 4
Nodes = 3
Stable service endpoint = web-service
Persistent dependency = managed database
~~~

Initial placement:

~~~text
Node A
- Replica 1
- Replica 2

Node B
- Replica 3

Node C
- Replica 4
~~~

## 1. Desired vs Observed State

Initial state:

~~~text
Desired = 4
Observed = 4
~~~

Then Replica 3 crashes.

Model:

~~~text
Desired = 4
Observed = 3
→ controller detects difference
→ replacement requested
~~~

Explain why reconciliation is a loop rather than a one-time command.

## 2. Scheduler Reasoning

Assume a replacement replica must be scheduled.

Available node capacity:

~~~text
Node A: 10% free CPU, 15% free memory
Node B: 60% free CPU, 55% free memory
Node C: 20% free CPU, 70% free memory
~~~

The workload requires moderate CPU and memory.

Discuss:

- which node appears suitable
- what additional constraints may matter
- why free capacity alone is not enough
- what happens if no node satisfies requirements

## 3. Unschedulable Scenario

Now assume every node lacks enough capacity.

Explain:

~~~text
Desired replicas = 4
Observed replicas = 3
Replacement requested
No suitable node
→ workload remains pending / unscheduled
~~~

Explain why:

> "The orchestrator will self-heal it"

is incomplete without capacity.

## 4. Service Discovery

Replicas have changing instance addresses.

Model:

~~~text
Client
→ Stable Service Identity
→ Healthy Replica Set
→ Replica A / B / C / D
~~~

Explain why clients should not manually track replica addresses.

## 5. Load Balancing

Discuss what the load-balancing layer needs to know:

- which replicas exist
- which replicas are ready
- which replicas should receive traffic

Explain why a running-but-not-ready replica should not necessarily receive traffic.

## 6. Node Failure

Now Node A fails.

Two replicas disappear together.

Observed state:

~~~text
Desired = 4
Observed = 2
~~~

Analyze:

- blast radius
- replacement demand
- remaining cluster capacity
- service availability
- dependency health
- recovery time

## 7. Failure-Domain Reasoning

Compare:

### Placement A

~~~text
Node A: 4 replicas
Node B: 0
Node C: 0
~~~

### Placement B

~~~text
Node A: 2
Node B: 1
Node C: 1
~~~

Explain why replica count alone does not guarantee availability.

## 8. Stateful Workload Variant

Now assume each replica requires unique persistent identity and storage.

Explain why:

~~~text
"Just start a replacement anywhere"
~~~

may no longer be sufficient.

Discuss:

- storage attachment
- identity
- ordering
- consistency
- recovery

## 9. Rolling Update

Assume version v1 has four replicas.

Target is v2.

Model:

~~~text
v1 v1 v1 v1
→ v2 v1 v1 v1
→ v2 v2 v1 v1
→ v2 v2 v2 v1
→ v2 v2 v2 v2
~~~

Now assume v2 fails readiness checks.

Explain:

- what the orchestrator can detect
- why deployment should stop or slow
- why readiness is part of rollout safety
- why runtime verification is still needed

## 10. Self-Healing Boundary

Classify each condition as:

~~~text
Likely Platform-Recoverable
Needs Capacity
Needs Human/Application Fix
Needs External Dependency Recovery
~~~

Conditions:

- one process crashes
- one node fails
- image cannot be pulled
- cluster has no spare capacity
- bad application configuration
- database unavailable
- persistent volume cannot attach
- control plane unavailable

## 11. Evidence Correlation

For a failed rollout, correlate:

~~~text
Application Logs
Container Status
Health/Readiness
Scheduler Events
Node Metrics
Network Evidence
Storage Events
Deployment Version
~~~

Explain why troubleshooting should not start by assuming one layer.

## 12. Senior Engineer Connection

Use:

~~~text
Impact
→ Desired State
→ Observed State
→ Placement
→ Capacity
→ Health
→ Service Discovery
→ Dependencies
→ Recovery
~~~

## 13. SRE Connection

Connect this scenario to:

- availability
- saturation
- rescheduling time
- replica health
- SLO impact
- blast radius
- alerting quality

## 14. Architect Connection

Design decisions should consider:

- replica spread
- failure domains
- spare capacity
- state placement
- service abstraction
- rollout strategy
- recovery assumptions

## Validation Checklist

- [ ] Modeled desired vs observed replicas
- [ ] Explained reconciliation
- [ ] Reasoned about scheduling constraints
- [ ] Explained unschedulable workload behavior
- [ ] Designed service-discovery flow
- [ ] Analyzed node-level blast radius
- [ ] Compared replica placement models
- [ ] Explained stateful recovery complexity
- [ ] Analyzed rolling-update readiness failure
- [ ] Defined self-healing boundaries

## Teach-Back

Explain:

> "Orchestration can reconcile desired state, but recovery still depends on capacity, health, storage, networking, dependencies, and control-plane availability."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
