---
id: EXP-D00-008
domain: D00
topics:
  - D00-T006
level: L2-L3
type: experiment
status: draft
estimated_time: 50-70m
environment:
  - Local workstation
  - Spreadsheet or text editor optional
  - No cloud account required
evidence_status:
  - DRAFT
---

# EXP-D00-008 — Model Autoscaling, Quotas, Cost, and Blast Radius

## Objective

Reason about cloud scaling decisions without creating live infrastructure.

This experiment demonstrates that autoscaling is constrained by:

- policy
- workload architecture
- quotas
- downstream dependencies
- cost
- failure domains

## Safety

No live cloud resources are created.

This is a simulation/reasoning exercise only.

## Scenario

A web service starts with:

~~~text
Minimum instances: 2
Maximum instances: 8
Current instances: 2
Target CPU: 60%
Traffic: 1,000 requests/minute
Database capacity: 4,000 requests/minute
Account quota: maximum 6 instances
Cost per instance-hour: 1 cost unit
~~~

Assume each healthy instance can handle approximately:

~~~text
700 requests/minute
~~~

before latency rises significantly.

These numbers are only for the exercise.

## 1. Baseline Capacity

Calculate:

~~~text
2 instances × 700 req/min
= 1,400 req/min theoretical app-tier capacity
~~~

Traffic is 1,000 req/min.

Questions:

1. Is there app-tier headroom?
2. Is database capacity currently a bottleneck?
3. What happens if one app instance fails?

## 2. Traffic Spike

Traffic rises to:

~~~text
3,500 requests/minute
~~~

Estimate required app instances:

~~~text
3,500 / 700 = 5 instances
~~~

Questions:

- Is that within autoscaling maximum?
- Is that within quota?
- Can the database handle the traffic?
- What is the new hourly instance cost?

## 3. Bigger Spike

Traffic rises to:

~~~text
5,000 requests/minute
~~~

The autoscaler wants:

~~~text
8 instances
~~~

But account quota allows only:

~~~text
6 instances
~~~

Questions:

1. What is the effective scaling ceiling?
2. What user impact might appear?
3. What metric could show saturation?
4. Why is "autoscaling enabled" not enough?

## 4. Dependency Bottleneck

Now suppose:

~~~text
Database safe capacity = 4,000 req/min
App tier can scale beyond that
~~~

Ask:

> What happens if the app tier keeps scaling while the database is already saturated?

Potential effects:

- more database connections
- more queued work
- higher latency
- more retries
- higher cost
- worse failure propagation

## 5. Cost Model

Fill this table:

| Instances | Approx App Capacity | Cost Units / Hour |
|---:|---:|---:|
| 2 | | |
| 4 | | |
| 5 | | |
| 6 | | |

Then explain:

> Autoscaling is both a capacity mechanism and a cost mechanism.

## 6. Failure-Domain Model

Assume six instances exist.

### Design A

~~~text
All 6 in one zone
~~~

### Design B

~~~text
3 in Zone A
3 in Zone B
~~~

Questions:

1. Which design has a larger zone-failure blast radius?
2. If Zone A fails in Design B, how much application capacity remains?
3. Is remaining database capacity also independent?
4. What additional evidence is required before claiming high availability?

## 7. Blast Radius Exercise

Classify the potential blast radius of:

- one failed instance
- one bad autoscaling policy
- one zone failure
- one account-wide IAM mistake
- one shared database outage
- one incorrect IaC change applied to all environments

Use:

~~~text
Local
Service
Zone
Environment
Account / Project
Multi-environment
Organization
~~~

## 8. Governance Connection

Add guardrails for the scenario:

- autoscaling maximum
- quota alert
- budget alert
- approved zones
- tagging
- least privilege
- change review
- database-capacity alert

## 9. SRE Connection

Useful signals include:

- request rate
- latency
- error rate
- saturation
- instance count
- scaling activity
- quota consumption
- dependency latency
- cost anomaly

## 10. Architect Connection

A good scaling design asks:

~~~text
Can app scale?
Can state scale?
Can database scale?
Can network scale?
Can quotas allow it?
Can budget allow it?
Can failure domains tolerate it?
~~~

## Validation Checklist

- [ ] Calculated baseline app capacity
- [ ] Modeled a traffic spike
- [ ] Identified quota as a scaling constraint
- [ ] Identified database as a downstream capacity constraint
- [ ] Calculated simple cost impact
- [ ] Compared one-zone vs two-zone blast radius
- [ ] Proposed governance guardrails

## Teach-Back

Explain why:

> "We use autoscaling, so capacity is solved"

is an unsafe architecture assumption.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after the exercise is completed and reviewed.
