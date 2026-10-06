# D00-T006 — Applied Cloud Scenario

## Scenario

A customer-facing API runs in a public cloud.

Architecture:

~~~text
Users
  ↓
Cloud Load Balancer
  ↓
Autoscaled App Tier
  ↓
Managed Database
  ↓
Object Storage
~~~

Current configuration:

~~~text
Minimum app instances: 2
Maximum app instances: 10
Current app instances: 4
App instance quota: 6
Deployment: one region, one zone
Database: managed service
Traffic: increasing rapidly
Application state: local session memory
Object storage: regional
Recent change: autoscaling policy changed
Cloud bill: rising sharply
~~~

Observed during an incident:

~~~text
User latency: high
Error rate: elevated
App CPU: 40%
App instance count: 6
Autoscaler wants: 9
Database latency: elevated
Quota errors: observed
Cloud management API: healthy
Load balancer: reachable
Some users lose sessions when requests reach different instances
Cost anomaly alert: triggered
~~~

## Task 1 — Control Plane vs Data Plane

Classify:

- changing the autoscaling policy
- creating new app instances
- users sending API requests
- the managed database processing application queries
- reading objects from object storage

Then answer:

> Does a healthy cloud management API prove the application data path is healthy?

## Task 2 — Autoscaling Diagnosis

The autoscaler wants 9 instances, but only 6 exist.

Explain:

- why
- what evidence supports a quota ceiling
- why autoscaling is not solving latency
- why app CPU at 40% does not rule out a dependency bottleneck

## Task 3 — State Placement

Users lose sessions after horizontal scaling.

Explain:

- why local session memory creates a scaling problem
- why sticky sessions may reduce symptoms but not remove the architectural coupling
- what externalized-state options could change the behavior
- what new dependency externalized state creates

## Task 4 — Dependency Capacity

Database latency is elevated.

Explain why adding more app instances can make the system worse.

Consider:

- connection growth
- request concurrency
- retry behavior
- database saturation
- cost

## Task 5 — Failure-Domain Reasoning

All app instances run in one zone.

Explain:

- the zone-level blast radius
- why multiple instances do not eliminate zone risk
- what changes in a two-zone design
- why two-zone design is still not automatically disaster recovery

## Task 6 — Shared Responsibility

The database is managed.

Separate likely provider vs customer responsibilities for:

- physical hardware
- database platform patching
- schema design
- credentials/access policy
- application retry logic
- data classification
- backup/recovery requirements
- query/index design

## Task 7 — Cost and Governance

The bill is rising.

Identify at least five cost/governance controls relevant to the scenario.

Examples may include:

- autoscaling max
- budget alert
- quota review
- tagging
- environment ownership
- policy
- idle-resource review
- data-transfer awareness

## Task 8 — Senior Engineer Response

Write an investigation sequence:

~~~text
Impact
→ Data Path
→ App Tier
→ State Placement
→ Quota / Scaling
→ Database / Dependencies
→ Failure Domain
→ Cost / Governance
→ Safe Mitigation
→ Root Cause
→ Prevention
~~~

## Task 9 — SRE View

Answer:

1. Which user-facing SLIs are degraded?
2. Which signals indicate saturation despite moderate CPU?
3. Which scaling and quota signals should be monitored?
4. What is the blast radius of the one-zone design?
5. Which control-plane changes should be correlated with the incident?

## Task 10 — Architect View

The business wants 10x traffic growth and improved availability.

Evaluate:

- service model
- state placement
- autoscaling
- quota management
- database scaling
- zone strategy
- region/DR strategy
- observability
- identity
- governance
- cost
- portability

Do not answer with "use more cloud services" or "use multi-cloud" without requirements and trade-offs.

## Success Standard

A strong response identifies at least four separate constraints:

- quota ceiling
- local session state
- database bottleneck
- single-zone blast radius

It also explains why moderate CPU and healthy control-plane APIs do not prove the system is healthy.
