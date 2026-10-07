---
id: EXP-D00-015
domain: D00
topics:
  - D00-T010
level: L2-L3
type: experiment
status: draft
estimated_time: 50-70m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-015 — Ephemeral vs Persistent State, Health, and Restart Reasoning

## Objective

Reason about workload state, storage lifecycle, health signals, and restart behavior without deploying a real container platform.

## Safety

This is a local architecture exercise.

No production system, cluster, privileged runtime, or destructive command is required.

## Scenario

A containerized service writes:

~~~text
/app/cache/session.tmp
/app/uploads/customer-photo.jpg
/app/logs/app.log
~~~

The service also uses:

~~~text
Managed Database
Persistent Volume
Central Log Platform
~~~

The container is later replaced.

## 1. Classify Data

Classify each item:

~~~text
Ephemeral
Persistent
External Durable State
Operational Evidence
Unknown / Needs Design
~~~

Items:

- temporary session cache
- customer upload
- application log file inside container
- database record
- persistent-volume file
- image filesystem layer
- environment variable
- runtime secret

## 2. Container Recreation

Assume the original container disappears and a new container starts from the same image.

For each data item, ask:

- should it survive?
- where should it live?
- who owns its lifecycle?
- what happens if it is missing?

## 3. Writable Layer Reasoning

Explain:

~~~text
Image Layers
+
Writable Container Layer
→ Runtime Filesystem View
~~~

Then explain why writable container state should not automatically be treated as durable.

## 4. Persistent Storage Boundary

Model:

~~~text
Replaceable Workload
↔
Persistent Storage
~~~

Explain why storage lifecycle and workload lifecycle must be reasoned about separately.

## 5. Health Questions

Classify each question:

~~~text
Startup
Liveness
Readiness
Business / Service Health
~~~

Questions:

1. Has the application finished initialization?
2. Should the process be restarted?
3. Should traffic be sent to this instance?
4. Is p95 latency within the SLO?
5. Is the downstream database available?
6. Is the application process running?

Explain why no single probe answers every health question.

## 6. Restart Loop Scenario

Assume:

~~~text
Container starts
→ configuration invalid
→ process exits
→ orchestrator restarts
→ process exits
→ restart repeats
~~~

Explain:

- what restart automation is accomplishing
- what it is not fixing
- what evidence should be preserved
- when repeated restart becomes a troubleshooting signal

## 7. Readiness Failure Scenario

Assume the process is alive but cannot connect to its required database.

Discuss whether it should:

- stay running
- receive traffic
- be restarted immediately
- emit a dependency-health signal

Explain your reasoning.

## 8. Data-Loss Scenario

Assume customer uploads were stored only in the container writable layer.

The container is replaced.

Explain:

- what likely happens to those uploads
- which design assumption failed
- how the architecture should change

## 9. Observability Design

Decide which evidence should survive container replacement:

- application logs
- metrics
- events
- deployment/version identity
- crash reason

Explain why centralized evidence matters for ephemeral workloads.

## 10. Senior Engineer Connection

A senior engineer should ask:

~~~text
What is ephemeral?
What must survive?
What is the workload lifecycle?
What is the storage lifecycle?
Which health question are we actually asking?
Why is the process restarting?
~~~

## 11. SRE Connection

Connect restart loops and readiness failures to:

- availability
- error rate
- latency
- alert quality
- recovery behavior
- operational toil

## 12. Architect Connection

Design boundaries for:

- replaceable compute
- durable data
- logs/telemetry
- secrets
- configuration
- dependency health

## Validation Checklist

- [ ] Classified ephemeral vs persistent data
- [ ] Explained writable-layer lifecycle
- [ ] Separated workload lifecycle from storage lifecycle
- [ ] Distinguished startup/liveness/readiness
- [ ] Analyzed a restart loop
- [ ] Reasoned about dependency health
- [ ] Designed evidence retention

## Teach-Back

Explain:

> "Containers are replaceable; durable state and troubleshooting evidence must be designed to survive replacement."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
