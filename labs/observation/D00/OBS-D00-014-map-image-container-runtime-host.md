---
id: OBS-D00-014
domain: D00
topics:
  - D00-T010
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# OBS-D00-014 — Map Image → Container → Runtime → Host

## Objective

Build a clear mental model of the layers involved when a containerized application runs.

The learner should be able to separate:

~~~text
Image
Container
Runtime
Host OS / Kernel
Infrastructure
~~~

without treating a container as a virtual machine.

## Why This Matters

Many troubleshooting mistakes happen because engineers collapse all container layers into one idea.

A useful first question is:

> Which layer owns the problem?

## Safety

This is a local reasoning and diagramming exercise.

No privileged container runtime, cloud account, cluster, or production access is required.

## Scenario

Assume an application is delivered as:

~~~text
customer-api:v3
~~~

The image contains:

- application binary
- language runtime
- required libraries
- startup command

The host provides:

- Linux kernel
- CPU
- memory
- filesystem
- networking
- container runtime

## 1. Build the Layer Diagram

Draw:

~~~text
Application Source
      ↓
Container Image
      ↓
Container Runtime
      ↓
Running Container Process
      ↓
Host Kernel
      ↓
CPU / Memory / Storage / Network
~~~

For each layer, write:

- what it owns
- what it does not own
- what failure it can create

## 2. Image vs Container

Complete:

| Question | Image | Container |
|---|---|---|
| Read-only packaged content? | | |
| Running process? | | |
| Can create many instances? | | |
| Has a lifecycle? | | |
| Has writable runtime state? | | |
| Identified by digest/content? | | |

Explain why:

> One image can create many containers.

## 3. Tag vs Digest

Assume:

~~~text
customer-api:latest
customer-api@sha256:abc123...
~~~

Explain:

- which is a movable name
- which identifies exact content
- why production traceability should prefer immutable identity where possible

## 4. Container vs VM

Build a comparison table:

| Concern | Container | Virtual Machine |
|---|---|---|
| Kernel | | |
| Isolation boundary | | |
| Startup overhead | | |
| Guest OS required | | |
| Host dependency | | |

Explain why "container = lightweight VM" is an incomplete model.

## 5. Runtime vs Orchestrator

Classify each responsibility:

~~~text
Create container process
Pull image
Start/stop container
Choose which node should run workload
Maintain desired replica count
Expose stable service identity
Restart failed container according to policy
~~~

Use:

~~~text
Runtime
Orchestrator
Shared / Depends on Architecture
~~~

## 6. Host Failure Reasoning

Assume five containers run on one host.

Then the host fails.

Explain:

- why all five workloads can be affected together
- why container isolation does not remove host failure
- what an orchestrator may attempt next
- what additional capacity is required for recovery

## 7. Evidence Mapping

For each failure, identify the likely first evidence source:

- image cannot be pulled
- process exits immediately
- host memory exhausted
- application port not listening
- node unavailable

Use:

~~~text
Image / Registry
Container Runtime
Application Logs
Host Metrics
Orchestrator Events
Network Evidence
~~~

## 8. Senior Engineer Connection

A senior engineer should separate:

~~~text
Artifact Problem
vs
Runtime Problem
vs
Host Problem
vs
Orchestrator Problem
~~~

before choosing commands or tools.

## 9. SRE Connection

Connect the layer model to blast radius:

~~~text
Container failure
< Host failure
< Shared platform/control-plane failure
~~~

Explain why the exact impact still depends on architecture.

## 10. Architect Connection

Ask:

- what isolation boundary is required?
- which failures should be independent?
- how many workloads should share one host/failure domain?
- what evidence must survive container replacement?

## Validation Checklist

- [ ] Distinguished image from container
- [ ] Distinguished runtime from orchestrator
- [ ] Explained shared-kernel model
- [ ] Compared container and VM boundaries
- [ ] Explained tag vs digest
- [ ] Reasoned about host-level blast radius
- [ ] Mapped failure evidence to layers

## Teach-Back

Explain:

> "A container is an isolated process workload running on a host; it is not a miniature standalone machine."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completing and reviewing the exercise.
