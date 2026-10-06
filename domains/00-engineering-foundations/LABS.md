
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

## Future D00 Practical Catalog

Future experiments include stateful/stateless behavior, manual vs automated work and partial failure.

Core Build-Break-Fix exercises include wrong port, instance failure, bad deployment configuration and dependency failure.

Troubleshooting challenges include application down, hidden dependency failure and capacity vs failure.

The Domain 00 capstone is CAP-D00-001 — The Production Application Is Slow.

Actual lab files live under the global [Labs](../../labs/README.md) system so one lab can serve multiple topics.
