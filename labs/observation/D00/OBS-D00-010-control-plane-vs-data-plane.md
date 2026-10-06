---
id: OBS-D00-010
domain: D00
topics:
  - D00-T006
level: L1-L2
type: observation
status: draft
estimated_time: 35-50m
environment:
  - Local workstation
  - No cloud account required
evidence_status:
  - DRAFT
---

# OBS-D00-010 — Map Control Plane vs Data Plane Actions

## Objective

Build a clear mental model of the difference between:

- management/configuration actions
- workload/data-serving actions

without creating any paid cloud resources.

## Why This Matters

Cloud incidents become confusing when engineers mix up:

~~~text
"Can I manage the resource?"
with
"Can the resource still serve workload traffic?"
~~~

Control-plane and data-plane paths can fail differently.

## Safety

This is a local reasoning and documentation exercise.

No cloud account, payment method, or live resource creation is required.

## Prerequisites

- D00-T006
- text editor
- shell optional

## 1. Start with a Simple Cloud Resource

Use a hypothetical load balancer.

### Control-Plane Actions

Examples:

- create load balancer
- update listener
- change health-check configuration
- attach backend
- delete load balancer

### Data-Plane Actions

Examples:

- accept user request
- forward request to backend
- return response to client

## 2. Create the Map

Write:

~~~text
Engineer / Automation
        ↓
Cloud API
        ↓
Control Plane
        ↓
Resource Configuration

User
 ↓
Data Plane Resource
 ↓
Application Backend
 ↓
Response
~~~

## 3. Classify Actions

Create a table:

| Action | Control Plane | Data Plane | Why |
|---|---:|---:|---|
| Create VM | | | |
| SSH/RDP/application traffic to VM | | | |
| Create object bucket | | | |
| Read object | | | |
| Change firewall rule | | | |
| Send application request | | | |
| Change autoscaling policy | | | |
| Process queued work | | | |

Do not memorize provider product names. Classify by purpose.

## 4. Failure Thought Experiment

Scenario:

~~~text
Cloud management API is temporarily unavailable.
Existing application instances are still running.
Users can still reach the application.
~~~

Answer:

1. Which plane is degraded?
2. Which plane is still serving?
3. What operations become difficult?
4. What operational risk appears if a new instance is needed during the outage?

## 5. Reverse Scenario

Scenario:

~~~text
Cloud portal/API works normally.
The application's data path is failing.
~~~

Answer:

1. Which plane appears healthy?
2. Which plane is failing?
3. Why would "portal is working" not prove application health?

## 6. Senior Engineer Connection

During troubleshooting, explicitly ask:

~~~text
Management path healthy?
Workload path healthy?
Both?
Neither?
~~~

## 7. SRE Connection

User-facing SLIs normally reflect the workload/data path, not whether an engineer can open the cloud console.

## 8. Architect Connection

Critical operations should account for:

- management-plane dependency
- recovery actions
- automation dependency
- workload/data-plane continuity

## Validation Checklist

- [ ] Classified at least eight actions
- [ ] Explained control plane in your own words
- [ ] Explained data plane in your own words
- [ ] Reasoned through control-plane-only failure
- [ ] Reasoned through data-plane-only failure
- [ ] Connected the distinction to incident response

## Teach-Back

Explain this sentence:

> "The cloud API can be down while some workloads continue serving traffic."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after the exercise is completed and reviewed.
