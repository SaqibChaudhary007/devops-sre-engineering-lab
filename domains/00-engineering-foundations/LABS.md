
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

## 00.11 — Distributed Systems Foundations

1. [OBS-D00-015 — Diagnose an Ambiguous Timeout](../../labs/observation/D00/OBS-D00-015-diagnose-ambiguous-timeout.md)
2. [EXP-D00-017 — Retry, Duplicate Work, Idempotency, and Retry Amplification](../../labs/experiments/D00/EXP-D00-017-retry-idempotency-amplification.md)
3. [EXP-D00-018 — Replication, Partition Trade-Offs, Backpressure, and Failure Domains](../../labs/experiments/D00/EXP-D00-018-replication-partition-backpressure-failure-domains.md)

These assets turn distributed-systems mental models into provider-neutral reasoning exercises for ambiguous timeouts, safe retries, request identity, duplicate side effects, retry amplification, backoff/jitter, circuit breakers, replication lag, stale reads, CAP partition-time trade-offs, queue backlog, backpressure, hot partitions, failure-domain placement, graceful degradation, and cross-service observability.

### Verification Status

All D00-T011 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.12 — Reliability Engineering Foundations

1. [OBS-D00-016 — Map a Critical User Journey and Reliability Boundaries](../../labs/observation/D00/OBS-D00-016-map-critical-user-journey-reliability-boundaries.md)
2. [EXP-D00-019 — Reliability Targets, Failure Domains, Redundancy, and Graceful Degradation](../../labs/experiments/D00/EXP-D00-019-reliability-targets-failure-domains-degradation.md)
3. [EXP-D00-020 — Recovery, Capacity Headroom, Backup Validation, and Incident Timeline](../../labs/experiments/D00/EXP-D00-020-recovery-capacity-backup-incident-timeline.md)

These assets turn reliability-engineering foundations into provider-neutral reasoning exercises for critical user journeys, reliability properties, failure domains, blast radius, redundancy independence, graceful degradation, SLI/SLO/SLA mental models, error budgets, failover assumptions, capacity headroom, saturation, alert quality, RTO/RPO, tested recovery, runbooks, and production readiness.

### Verification Status

All D00-T012 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.13 — SRE Foundations

1. [OBS-D00-017 — Map a User Journey to SLI, SLO, and Alerting Decisions](../../labs/observation/D00/OBS-D00-017-user-journey-sli-slo-alerting.md)
2. [EXP-D00-021 — Error Budget, Toil, Automation, and Safe Change Decisions](../../labs/experiments/D00/EXP-D00-021-error-budget-toil-automation-safe-change.md)
3. [EXP-D00-022 — Incident Response, Alert Actionability, Postmortem, and Production Readiness](../../labs/experiments/D00/EXP-D00-022-incident-alert-postmortem-production-readiness.md)

These assets turn SRE foundations into provider-neutral reasoning exercises for user journeys, service boundaries, SLI/SLO/SLA, error-budget decisions, page/ticket/dashboard classification, alert actionability, toil, automation boundaries, safe change, on-call feedback, incident timelines, mitigation vs permanent correction, postmortem learning, blameless analysis, release safety, and production readiness.

### Verification Status

All D00-T013 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.14 — Observability Foundations

1. [OBS-D00-018 — Map a User Journey to Metrics, Logs, Traces, and Events](../../labs/observation/D00/OBS-D00-018-map-user-journey-observability-signals.md)
2. [EXP-D00-023 — Cardinality, Tail Latency, Sampling, and Telemetry Cost](../../labs/experiments/D00/EXP-D00-023-cardinality-latency-sampling-cost.md)
3. [EXP-D00-024 — Evidence-First Incident Investigation and Dashboard Review](../../labs/experiments/D00/EXP-D00-024-evidence-first-incident-dashboard-review.md)

These assets turn observability foundations into provider-neutral reasoning exercises for user journeys, telemetry mapping, metrics/logs/traces/events, structured logging, context propagation, black-box vs white-box evidence, business/dependency/queue signals, cardinality, tail latency, aggregation, sampling, retention, telemetry cost, security/privacy, dashboard hierarchy, alert context, change markers, and evidence-first troubleshooting.

### Verification Status

All D00-T014 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## 00.15 — Security Foundations

1. [OBS-D00-019 — Map Assets, Threats, Trust Boundaries, and Controls](../../labs/observation/D00/OBS-D00-019-assets-trust-boundaries-controls.md)
2. [EXP-D00-025 — Identity, Least Privilege, Secrets, and Audit Review](../../labs/experiments/D00/EXP-D00-025-identity-least-privilege-secrets-audit.md)
3. [EXP-D00-026 — Supply-Chain Trust, Defense in Depth, and Security Readiness](../../labs/experiments/D00/EXP-D00-026-supply-chain-defense-security-readiness.md)

These assets turn Security Foundations into safe, provider-neutral reasoning exercises for assets/threats/vulnerabilities/risk, trust boundaries, authentication vs authorization, least privilege, human/workload identity, secrets lifecycle, auditability, CI/CD trust, artifact integrity/provenance, dependency risk, defense in depth, blast radius, backup security, security monitoring, security/reliability trade-offs, and production readiness.

### Verification Status

All D00-T015 practical assets are **DRAFT**, not LAB-VERIFIED.

Promote them only after completing them end-to-end and reviewing the outputs.

## Future D00 Practical Catalog

Future experiments include stateful/stateless behavior, manual vs automated work and partial failure.

Core Build-Break-Fix exercises include wrong port, instance failure, bad deployment configuration and dependency failure.

Troubleshooting challenges include application down, hidden dependency failure and capacity vs failure.

The Domain 00 capstone is CAP-D00-001 — The Production Application Is Slow.

Actual lab files live under the global [Labs](../../labs/README.md) system so one lab can serve multiple topics.
