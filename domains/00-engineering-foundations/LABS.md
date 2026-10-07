
# D00 Labs / Build-Break-Fix / Troubleshooting

## Practical Lifecycle

~~~text
Observe
→ Build
→ Validate
→ Break
→ Troubleshoot
→ Recover
→ Improve
~~~

## Asset Types

- OBS — Observation
- EXP — Experiment
- LAB — Build
- BBF — Build-Break-Fix
- TS — Blind Troubleshooting
- INC — Incident Simulation
- ARCH — Architecture Exercise
- TEACH — Teach-Back
- CAP — Capstone

## 00.01 — How Computers Work

1. [OBS-D00-001 — Observe System Resources](../../labs/observation/D00/OBS-D00-001-observe-system-resources.md)
2. [OBS-D00-002 — Observe a Process](../../labs/observation/D00/OBS-D00-002-observe-a-process.md)
3. [EXP-D00-001 — Resource Consumption Experiment](../../labs/experiments/D00/EXP-D00-001-resource-consumption.md)

## 00.02 — Operating System Mental Model

1. [OBS-D00-003 — Observe the Operating System Boundary](../../labs/observation/D00/OBS-D00-003-observe-os-boundary.md)
2. [OBS-D00-004 — Observe System Calls](../../labs/observation/D00/OBS-D00-004-observe-system-calls.md)
3. [EXP-D00-002 — Process States, Scheduling and Waiting](../../labs/experiments/D00/EXP-D00-002-process-states-scheduling-waiting.md)

These practical assets connect kernel/user-space separation, process state, system calls, identity, permissions, scheduling and waiting to a real Linux system.

### Verification Status

All D00-T002 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after executing them end-to-end on supported environments.

## 00.03 — Software Engineering Foundations

1. [OBS-D00-005 — Observe Source → Runtime → Process](../../labs/observation/D00/OBS-D00-005-observe-source-runtime-process.md)
2. [OBS-D00-006 — Compile Source and Inspect the Artifact](../../labs/observation/D00/OBS-D00-006-compile-and-inspect-artifact.md)
3. [EXP-D00-003 — Configuration, Startup Failure and Exit Status](../../labs/experiments/D00/EXP-D00-003-configuration-startup-exit-status.md)

These assets connect source code, runtime execution, compilation, artifacts, configuration and exit status to real Linux processes.

### Verification Status

All D00-T003 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after executing them end-to-end on supported environments.

## 00.04 — Application Architecture Fundamentals

1. [OBS-D00-007 — Trace a Request Through Client → API → Data](../../labs/observation/D00/OBS-D00-007-trace-client-api-data.md)
2. [EXP-D00-004 — Local State vs Replaceable Instances](../../labs/experiments/D00/EXP-D00-004-local-state-vs-replaceable-instances.md)
3. [EXP-D00-005 — Observe Synchronous Dependency Latency Propagation](../../labs/experiments/D00/EXP-D00-005-synchronous-dependency-latency.md)

These assets connect client/server request flow, state placement, horizontal scaling implications and dependency latency propagation to real local processes.

### Verification Status

All D00-T004 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after executing them end-to-end on supported environments.

## 00.05 — Infrastructure Foundations

1. [OBS-D00-008 — Inspect Compute, Memory, Storage, and Network Resources](../../labs/observation/D00/OBS-D00-008-inspect-infrastructure-resources.md)
2. [OBS-D00-009 — Detect Virtualization and Map Infrastructure Dependencies](../../labs/observation/D00/OBS-D00-009-detect-virtualization-map-dependencies.md)
3. [EXP-D00-006 — Capacity, Utilization, and Headroom with a Bounded Workload](../../labs/experiments/D00/EXP-D00-006-capacity-utilization-headroom.md)

These assets connect guest-visible compute, memory, storage, network, virtualization evidence, dependency mapping, failure domains, capacity, utilization, saturation, and headroom to a real Linux lab system.

### Verification Status

All D00-T005 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after executing them end-to-end on supported lab environments.

## 00.06 — Cloud Mental Models

1. [OBS-D00-010 — Map Control Plane vs Data Plane Actions](../../labs/observation/D00/OBS-D00-010-control-plane-vs-data-plane.md)
2. [EXP-D00-007 — Compare IaaS, PaaS, SaaS, and Serverless Responsibility Boundaries](../../labs/experiments/D00/EXP-D00-007-service-model-responsibility-boundaries.md)
3. [EXP-D00-008 — Model Autoscaling, Quotas, Cost, and Blast Radius](../../labs/experiments/D00/EXP-D00-008-autoscaling-quotas-cost-blast-radius.md)

These assets convert cloud abstractions into provider-neutral reasoning exercises for control/data planes, service-model responsibility, elasticity, quotas, dependency capacity, cost, governance, and blast radius without requiring paid cloud resources.

### Verification Status

All D00-T006 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after executing/completing them end-to-end and reviewing the results.

## 00.07 — DevOps Foundations

1. [OBS-D00-011 — Map a Change from Idea to Production and Feedback](../../labs/observation/D00/OBS-D00-011-map-change-idea-to-production.md)
2. [EXP-D00-009 — Compare Large-Batch vs Small-Batch Delivery](../../labs/experiments/D00/EXP-D00-009-large-vs-small-batch-delivery.md)
3. [EXP-D00-010 — Build a Delivery Metrics, Toil, and Feedback Worksheet](../../labs/experiments/D00/EXP-D00-010-delivery-metrics-toil-feedback.md)

These assets turn DevOps concepts into concrete, provider-neutral delivery-system reasoning: end-to-end flow, queues, handoffs, bottlenecks, feedback loops, batch-size trade-offs, the current DORA five-metric model, toil classification, recovery thinking, and metric-gaming risks.

### Verification Status

All D00-T007 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.08 — Infrastructure as Code Mental Model

1. [OBS-D00-012 — Desired State, Actual State, and Drift Mapping](../../labs/observation/D00/OBS-D00-012-desired-actual-state-drift.md)
2. [EXP-D00-011 — Dependency Graph, State Boundary, and Concurrency Design](../../labs/experiments/D00/EXP-D00-011-dependency-state-boundary-concurrency.md)
3. [EXP-D00-012 — Review a Hypothetical IaC Plan for Safety, Cost, and Recovery](../../labs/experiments/D00/EXP-D00-012-iac-plan-safety-cost-recovery-review.md)

These assets turn IaC mental models into provider-neutral reasoning exercises for desired vs actual state, drift, dependency graphs, ownership/state boundaries, concurrency, locking, change-plan review, replacement/deletion risk, security, cost, blast radius, and recovery.

### Verification Status

All D00-T008 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.09 — CI/CD Mental Model

1. [OBS-D00-013 — Trace a Change from Commit to Production Outcome](../../labs/observation/D00/OBS-D00-013-trace-commit-to-production-outcome.md)
2. [EXP-D00-013 — Build Once, Promote, Cache, and Artifact Integrity](../../labs/experiments/D00/EXP-D00-013-build-once-promote-artifact-integrity.md)
3. [EXP-D00-014 — Diagnose Pipeline Failure, Retry, Concurrency, and Recovery](../../labs/experiments/D00/EXP-D00-014-pipeline-failure-retry-concurrency-recovery.md)

These assets turn CI/CD mental models into provider-neutral reasoning exercises for end-to-end traceability, build-once/promote, artifact identity, cache vs artifact, provenance, flaky signals, retries, concurrency, protected production delivery, deployment verification, change markers, runner trust, and rollback/roll-forward recovery.

### Verification Status

All D00-T009 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.10 — Containers & Orchestration Mental Model

1. [OBS-D00-014 — Map Image → Container → Runtime → Host](../../labs/observation/D00/OBS-D00-014-map-image-container-runtime-host.md)
2. [EXP-D00-015 — Ephemeral vs Persistent State, Health, and Restart Reasoning](../../labs/experiments/D00/EXP-D00-015-ephemeral-persistent-health-restart.md)
3. [EXP-D00-016 — Desired Replicas, Scheduling, Service Discovery, and Failure Recovery](../../labs/experiments/D00/EXP-D00-016-replicas-scheduling-service-discovery-recovery.md)

These assets turn container/orchestration mental models into provider-neutral reasoning exercises for image/container/runtime/host boundaries, tag vs digest identity, container vs VM isolation, ephemeral vs persistent state, startup/liveness/readiness, restart loops, desired replicas, scheduler constraints, service discovery, node failure, rollout readiness, stateful recovery, and self-healing boundaries.

### Verification Status

All D00-T010 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## Future D00 Practical Catalog

Future experiments include stateful/stateless behavior, manual vs automated work and partial failure.

Core Build-Break-Fix exercises include wrong port, instance failure, bad deployment configuration and dependency failure.

Troubleshooting challenges include application down, hidden dependency failure and capacity vs failure.

The Domain 00 capstone is CAP-D00-001 — The Production Application Is Slow.

Actual lab files live under the global [Labs](../../labs/README.md) system so one lab can serve multiple topics.
