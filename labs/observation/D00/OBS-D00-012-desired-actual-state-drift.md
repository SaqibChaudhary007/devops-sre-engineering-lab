---
id: OBS-D00-012
domain: D00
topics:
  - D00-T008
level: L1-L2
type: observation
status: draft
estimated_time: 40-55m
environment:
  - Local workstation
  - Text editor or notebook
evidence_status:
  - DRAFT
---

# OBS-D00-012 — Desired State, Actual State, and Drift Mapping

## Objective

Build the core Infrastructure as Code mental model by comparing intended infrastructure with actual infrastructure and identifying drift without touching any real cloud or production system.

## Why This Matters

IaC is useful only when an engineer can reason about:

~~~text
Desired State
vs
Actual State
vs
Observed Difference
~~~

A definition can be correct while reality has changed.

A real environment can also be healthy while the code is stale.

The engineer must understand both.

## Safety

This is a documentation and reasoning exercise.

Do not connect to a production system, cloud account, or privileged environment.

## Scenario

Assume the desired infrastructure is:

~~~text
Environment: production

Network:
- private application subnet
- HTTPS ingress only

Application Tier:
- 3 instances
- instance size: medium
- managed by autoscaling group

Database:
- managed database
- encrypted storage
- backups enabled

Metadata:
- owner=payments
- environment=production
- criticality=high
~~~

Now assume the actual environment has these differences:

~~~text
- application instance count is 4
- one instance was created manually
- SSH from the internet was temporarily opened during an incident
- database backups remain enabled
- database storage encryption remains enabled
- one resource is missing the owner tag
- instance size is still medium
~~~

## 1. Build the Comparison Table

Create:

| Resource / Property | Desired | Actual | Match? | Drift Type | Risk |
|---|---|---|---|---|---|
| App instance count | | | | | |
| Extra manual instance | | | | | |
| HTTPS ingress | | | | | |
| SSH ingress | | | | | |
| DB encryption | | | | | |
| DB backups | | | | | |
| Owner tag | | | | | |
| Instance size | | | | | |

Classify drift using:

~~~text
No Drift
Configuration Drift
Unmanaged Resource
Metadata Drift
Security Drift
~~~

## 2. Separate Desired from Current Reality

Answer:

1. Which source tells you what should exist?
2. Which source tells you what does exist?
3. Why is neither source sufficient by itself during troubleshooting?
4. Why is a repository not the same as runtime truth?

## 3. Drift Severity

Classify each difference as:

~~~text
Low
Medium
High
Critical
~~~

Explain your reasoning.

Consider:

- security exposure
- cost
- availability
- compliance
- ownership
- future plan/apply behavior

## 4. Emergency Change Reasoning

Assume SSH was opened during an incident for emergency troubleshooting.

After the incident:

- should the change remain?
- should code be updated to match reality?
- should reality be changed back to match code?
- what evidence should be preserved?

Explain why emergency changes must eventually be reconciled.

## 5. Plan Thinking

Imagine the IaC definition is applied again.

For each drift item, predict one of:

~~~text
No Change
Update
Delete
Adopt / Import Needed
Manual Investigation Needed
~~~

Do not assume the IaC engine will always make the safest choice automatically.

## 6. Senior Engineer Connection

A senior engineer should ask:

~~~text
What should exist?
What actually exists?
What changed outside code?
What is the risk?
What will the next plan do?
~~~

## 7. SRE Connection

Explain how drift can affect:

- incident diagnosis
- change correlation
- recovery
- access control
- blast radius

## 8. Architect Connection

Ask:

- which changes are allowed outside IaC?
- what is the emergency-change process?
- how quickly must drift be reconciled?
- which resources need stronger policy enforcement?

## Validation Checklist

- [ ] Compared desired and actual state
- [ ] Identified all drift items
- [ ] Classified drift by type
- [ ] Classified drift by severity
- [ ] Explained emergency-change reconciliation
- [ ] Predicted possible next-plan behavior
- [ ] Connected drift to production risk

## Teach-Back

Explain:

> "Infrastructure as Code manages intent, but engineers still need to observe reality."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completing and reviewing the exercise.
