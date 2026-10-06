# D00-T006 — Teach-Back Assessment

## Goal

Demonstrate that you can explain cloud concepts without hiding behind provider product names.

## Task A — Beginner

Explain:

- what cloud changes
- why physical infrastructure still exists
- why cloud is more than "someone else's server"

Use one simple analogy.

## Task B — Engineer

Explain:

~~~text
Human / Automation
→ Cloud API
→ Control Plane
→ Resource

User Traffic
→ Data Plane
→ Application / Service
~~~

Then give one example where the control plane is degraded but the workload continues serving traffic.

## Task C — Senior Engineer

Explain why this statement is unsafe:

> "Autoscaling is enabled, so capacity is solved."

Include:

- quotas
- downstream dependencies
- state
- scale-up time
- failure domains
- cost

## Task D — SRE

Explain the difference between:

~~~text
Availability
Resilience
Backup
Disaster Recovery
~~~

Then explain why two zones do not automatically equal DR.

## Task E — Architect

Compare:

~~~text
IaaS
vs
PaaS
vs
SaaS
vs
Serverless
~~~

Discuss:

- control
- responsibility
- operational burden
- portability
- scaling
- security
- observability
- cost

## Cloud Model Challenge

Explain:

~~~text
Public
Private
Hybrid
Multi-Cloud
~~~

and state clearly which are formal NIST deployment-model categories and which are industry terminology.

## Failure-Domain Diagram Challenge

Draw from memory:

~~~text
Provider
↓
Region
↓
Zone
↓
Resource
↓
Application
↓
Dependency
~~~

Then add:

- one quota constraint
- one shared-responsibility boundary
- one autoscaling loop
- one blast-radius example
- one cost control

## Scoring

Score 1–5 for:

- correctness
- clarity
- cloud operating-model reasoning
- control/data-plane reasoning
- scaling/quota reasoning
- reliability reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.
