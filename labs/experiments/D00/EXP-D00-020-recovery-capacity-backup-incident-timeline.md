---
id: EXP-D00-020
domain: D00
topics:
  - D00-T012
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# EXP-D00-020 — Recovery, Capacity Headroom, Backup Validation, and Incident Timeline

## Objective

Practice reliability reasoning across detection, response, containment, recovery, capacity headroom, backup validation, RTO/RPO, and incident readiness.

## Safety

This is a local reasoning exercise.

No production access, live failover, destructive testing, or real traffic manipulation is required.

## Scenario

A service has:

~~~text
Normal load = 70% of safe capacity
One node = 30% of total capacity
Three application nodes
Database backups every 15 minutes
Recovery runbook exists but has never been tested
On-call alerts on CPU > 80%
~~~

At 10:00:

~~~text
One application node fails
Traffic redistributes
Remaining nodes approach saturation
Latency rises
Retries increase
Checkout success falls
Alert fires at 10:08
Team starts mitigation at 10:15
Service returns to acceptable state at 10:32
~~~

## 1. Build the Incident Timeline

Create:

~~~text
Failure Start
→ Detection
→ Response
→ Containment
→ Recovery
→ Validation
~~~

Record:

- 10:00 failure begins
- 10:08 alert
- 10:15 mitigation begins
- 10:32 service restored

Calculate conceptually:

- time to detect
- time to respond
- time to recover

Then explain why each interval matters.

## 2. Capacity Headroom

Before failure:

~~~text
70% of safe capacity used
~~~

After losing one node, discuss:

- whether remaining capacity can absorb the load
- how retry traffic changes the picture
- why normal utilization alone is not enough
- why maintenance/failover headroom matters

## 3. Saturation and Cascading Failure

Model:

~~~text
Node Loss
→ Less Capacity
→ Higher Utilization
→ Higher Latency
→ More Timeouts
→ More Retries
→ More Load
→ Greater Saturation
~~~

Identify where reliability controls could break the loop:

- load shedding
- retry limiting
- graceful degradation
- additional capacity
- backpressure

## 4. Alert Quality

Current alert:

~~~text
CPU > 80%
~~~

Improve the alert model by combining:

- checkout success
- latency
- saturation
- dependency health
- queue age
- retry rate

Explain why user-impact-aware alerts can be more actionable.

## 5. Recovery Objective

Assume the business states:

~~~text
RTO = 30 minutes
RPO = 15 minutes
~~~

Explain:

- what RTO means
- what RPO means
- why they are different
- whether a backup every 15 minutes automatically proves the RPO

## 6. Backup vs Proven Recovery

The team has backups every 15 minutes but has never restored one.

Classify:

~~~text
Backup Exists
Recovery Proven
Recovery Time Known
Data Integrity Proven
~~~

For each, mark:

~~~text
Yes
No
Unknown
~~~

Explain what a restore test should validate.

## 7. Failover Readiness

Before trusting automated failover, verify conceptually:

- failure detection
- standby health
- data freshness
- capacity
- routing
- permissions
- dependency readiness
- recovery validation

Explain why failover automation is not the same as failover confidence.

## 8. Rollback vs Roll-Forward

A deployment causes checkout failures.

Compare:

### Rollback

~~~text
Return to known-good version
~~~

### Roll-forward

~~~text
Deploy a corrective version
~~~

Discuss:

- data/schema compatibility
- speed
- reversibility
- operational confidence
- blast radius

## 9. Runbook Review

Create a minimal runbook structure:

~~~text
Trigger
Symptoms
Impact
Evidence
Decision Point
Safe Mitigation
Recovery
Validation
Escalation
~~~

Explain how runbooks reduce cognitive load during incidents.

## 10. Production Readiness Review

Score each area:

~~~text
Ready
Partially Ready
Not Ready
~~~

Areas:

- critical-user-journey SLI
- reliability target
- capacity headroom
- dependency map
- tested backup restore
- failover validation
- dashboards
- actionable alerts
- rollback/roll-forward plan
- on-call ownership
- runbook
- access permissions

## 11. Senior Engineer Connection

Use:

~~~text
Impact
→ Capacity
→ Failure Domain
→ Detection
→ Evidence
→ Safe Mitigation
→ Recovery
→ Validation
→ Prevention
~~~

## 12. SRE Connection

Connect the exercise to:

- time to detect
- time to respond
- time to recover
- SLO impact
- saturation
- retry pressure
- alert quality
- toil
- error-budget impact

## 13. Architect Connection

Design decisions should cover:

- required headroom
- tolerated failure
- recovery objectives
- backup/restore architecture
- failover model
- degradation strategy
- operational ownership

## Validation Checklist

- [ ] Built a detection-to-recovery timeline
- [ ] Reasoned about capacity headroom after failure
- [ ] Identified cascading saturation risks
- [ ] Improved alert quality
- [ ] Distinguished RTO from RPO
- [ ] Distinguished backup existence from proven recovery
- [ ] Evaluated failover readiness
- [ ] Compared rollback vs roll-forward
- [ ] Built a runbook outline
- [ ] Performed a production-readiness review

## Teach-Back

Explain:

> "Reliable recovery depends on measured detection, enough capacity, tested procedures, validated backups, clear ownership, and proof that service is actually restored."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
