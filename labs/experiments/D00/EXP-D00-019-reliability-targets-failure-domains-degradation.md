---
id: EXP-D00-019
domain: D00
topics:
  - D00-T012
level: L2-L3
type: experiment
status: draft
estimated_time: 55-75m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-019 — Reliability Targets, Failure Domains, Redundancy, and Graceful Degradation

## Objective

Reason about reliability targets, failure models, redundancy, correlated failure, graceful degradation, and the trade-off between reliability and cost.

## Safety

This is a local architecture exercise.

No production access, live failover, traffic generation, or destructive testing is required.

## Scenario

A customer-facing service runs:

~~~text
2 application replicas
1 database primary
1 database standby
1 external payment provider
1 recommendation service
~~~

The team claims:

~~~text
"We are highly available because we have replicas."
~~~

Additional facts:

~~~text
- both application replicas run on the same node
- database primary and standby use the same storage failure domain
- the payment provider has no fallback
- recommendation failure blocks checkout
- spare compute capacity is minimal
~~~

## 1. Define Reliability Targets

For these journeys:

- login
- browse catalog
- checkout
- view recommendations

Define a simple reliability target using:

~~~text
User Journey
→ Success Condition
→ Reliability Importance
→ Example SLI
→ Example SLO
~~~

Do not design a full production SLO policy.

Keep the exercise at mental-model level.

## 2. Reliability vs Availability vs Durability

Classify each scenario:

- API responds but returns incorrect order state
- service is unreachable for 10 minutes
- service is available but recently committed data is lost
- service degrades recommendations but checkout succeeds
- service recovers automatically after one replica fails

Use:

~~~text
Availability
Durability
Resilience
Recoverability
Correctness / Reliability
~~~

Explain why one incident can involve more than one property.

## 3. Correlated Redundancy

Compare:

### Design A

~~~text
Replica 1 — Node A
Replica 2 — Node A
~~~

### Design B

~~~text
Replica 1 — Node A
Replica 2 — Node B
~~~

Explain why "two replicas" is weak evidence without failure-domain independence.

Repeat the reasoning for:

~~~text
Database Primary
Database Standby
Shared Storage Failure Domain
~~~

## 4. Failure Model

Write a simple failure model for the service.

Include whether it should tolerate:

- one application process failure
- one node failure
- one zone failure
- one database instance failure
- recommendation-service failure
- payment-provider failure

For each, state:

~~~text
Tolerated
Degraded
Not Tolerated
Unknown / Needs Decision
~~~

## 5. Graceful Degradation

Current design:

~~~text
Recommendation Service Down
→ Checkout Fails
~~~

Redesign:

~~~text
Recommendation Service Down
→ Recommendations Hidden
→ Checkout Continues
~~~

Explain:

- why this improves reliability
- why graceful degradation is safe only when business correctness allows it
- which dependencies cannot simply be skipped

## 6. Reliability vs Cost

Compare:

### Option A

~~~text
Single Zone
Low Spare Capacity
Minimal Redundancy
Lower Cost
~~~

### Option B

~~~text
Multiple Failure Domains
Spare Capacity
Redundant Dependencies
Higher Cost / Complexity
~~~

Discuss:

- business criticality
- expected impact of failure
- recovery requirements
- operational complexity
- diminishing returns

## 7. SLI, SLO, SLA

For checkout, classify:

~~~text
SLI
SLO
SLA
~~~

Examples:

- measured successful-checkout ratio
- target of 99.9% successful checkout requests over a defined window
- external contractual commitment with business consequences

Explain why these terms should not be used interchangeably.

## 8. Error Budget — Conceptual

Assume:

~~~text
SLO = 99.9%
~~~

Explain conceptually:

~~~text
100% - 99.9%
→ allowed unreliability
~~~

Then discuss what an exhausted error budget might influence:

- release pace
- reliability work
- risk acceptance
- investigation priorities

Do not create policy automation at this stage.

## 9. Failover Assumptions

For a database standby, ask:

- how is failure detected?
- is the standby current enough?
- is capacity sufficient?
- can traffic be redirected?
- what permissions are required?
- how will success be validated?

Explain why:

> "We have a standby"

does not prove recoverability.

## 10. Senior Engineer Connection

Use:

~~~text
Critical Journey
→ Reliability Target
→ Failure Model
→ Failure Domains
→ Redundancy Independence
→ Degradation
→ Failover
→ Validation
~~~

## 11. SRE Connection

Connect the design to:

- SLI
- SLO
- error budget
- detection
- recovery time
- blast radius
- dependency reliability

## 12. Architect Connection

Make decisions about:

- which failures must be tolerated
- which dependencies need redundancy
- which features may degrade
- where spare capacity is required
- what additional reliability cost is justified

## Validation Checklist

- [ ] Defined simple flow-level reliability targets
- [ ] Distinguished reliability properties
- [ ] Identified correlated redundancy
- [ ] Wrote a failure model
- [ ] Designed graceful degradation
- [ ] Discussed reliability/cost trade-offs
- [ ] Distinguished SLI/SLO/SLA
- [ ] Explained error budget conceptually
- [ ] Evaluated failover assumptions

## Teach-Back

Explain:

> "Redundancy improves reliability only when the redundant paths are sufficiently independent and the system can actually detect, fail over, and validate recovery."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
