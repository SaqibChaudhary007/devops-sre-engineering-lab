---
id: D00-T012
domain: D00
title: Reliability Engineering Foundations
level:
  - L1
  - L2
  - L3
priority: P1
status: published
estimated_time:
  theory: 6-8h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
    - D00-T003
    - D00-T004
    - D00-T005
    - D00-T006
    - D00-T007
    - D00-T008
    - D00-T009
    - D00-T010
    - D00-T011
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Five Levels
  - Production Room
  - Architecture With Saqib
---

# 00.12 — Reliability Engineering Foundations

## Start Here

You now understand how systems are built, delivered, containerized, orchestrated, and distributed.

The next question is:

> How do we design and operate systems so they continue delivering acceptable service even when components fail, traffic changes, deployments go wrong, dependencies degrade, or capacity is exhausted?

That is the problem space of **reliability engineering**.

Reliability is not:

- zero failure
- maximum redundancy everywhere
- 100% uptime
- only monitoring
- only backups
- only incident response
- the same as availability
- the same as disaster recovery

The core mental model is:

~~~text
User Expectation
→ Reliability Target
→ Failure Model
→ Prevention
→ Detection
→ Containment
→ Recovery
→ Learning
→ Improvement
~~~

Reliability engineering accepts that failure is normal and focuses on controlling **frequency, impact, duration, detectability, and recoverability**.

This topic stays at the D00 mental-model level. Formal SRE practices, error-budget policy, detailed SLO engineering, incident command, capacity models, chaos engineering, disaster recovery, and platform-specific reliability implementation come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- reliability
- availability
- durability
- resilience
- fault tolerance
- recoverability
- user-visible service
- critical user journey
- failure mode
- failure domain
- blast radius
- redundancy
- graceful degradation
- failover
- recovery
- RTO and RPO at a high level
- SLI, SLO, and SLA at a high level
- error budgets at a high level
- reliability target
- reliability vs cost
- dependency reliability
- end-to-end reliability
- redundancy vs independence
- active/active and active/passive at a high level
- health and readiness
- detection time
- response time
- recovery time
- MTTR at a high level
- MTBF / MTTF cautions at a high level
- change failure
- safe deployment
- rollback vs roll-forward
- capacity headroom
- saturation
- load shedding
- backpressure
- observability
- alert quality
- runbooks
- incident readiness
- backup vs recovery
- disaster recovery preview
- chaos / failure testing preview
- toil and human reliability
- production readiness
- Senior/SRE/Architect reasoning

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)
- [00.04 — Application Architecture Fundamentals](../00-04-application-architecture-fundamentals/README.md)
- [00.05 — Infrastructure Foundations](../00-05-infrastructure-foundations/README.md)
- [00.06 — Cloud Mental Models](../00-06-cloud-mental-models/README.md)
- [00.07 — DevOps Foundations](../00-07-devops-foundations/README.md)
- [00.08 — Infrastructure as Code Mental Model](../00-08-infrastructure-as-code-mental-model/README.md)
- [00.09 — CI/CD Mental Model](../00-09-cicd-mental-model/README.md)
- [00.10 — Containers & Orchestration Mental Model](../00-10-containers-orchestration-mental-model/README.md)
- [00.11 — Distributed Systems Foundations](../00-11-distributed-systems-foundations/README.md)

You should already understand partial failure, retries, dependencies, blast radius, failure domains, capacity, deployment risk, and production observability.

---

# Learning Package Navigation

Use this page as the canonical learner entry point.

Move through the package in this order:

1. **Learn** — complete the conceptual sections on this page.
2. **Verify** — review the [D00-T012 Source Verification](../../../../docs/sources/D00/D00-T012-source-verification.md).
3. **Visualize** — review the [D00-T012 Visual Package](../../../../docs/diagrams/D00/D00-T012/README.md).
4. **Observe the User Journey** — complete [OBS-D00-016 — Map a Critical User Journey and Reliability Boundaries](../../../../labs/observation/D00/OBS-D00-016-map-critical-user-journey-reliability-boundaries.md).
5. **Experiment with Reliability Targets & Failure Domains** — complete [EXP-D00-019 — Reliability Targets, Failure Domains, Redundancy, and Graceful Degradation](../../../../labs/experiments/D00/EXP-D00-019-reliability-targets-failure-domains-degradation.md).
6. **Experiment with Recovery & Capacity** — complete [EXP-D00-020 — Recovery, Capacity Headroom, Backup Validation, and Incident Timeline](../../../../labs/experiments/D00/EXP-D00-020-recovery-capacity-backup-incident-timeline.md).
7. **Assess** — complete the [D00-T012 Assessment Package](../../../../assessments/topics/D00/D00-T012/README.md).
8. **Teach Back** — explain reliability engineering at Beginner, Engineer, Senior, SRE, and Architect levels.
9. **Continue** — move to 00.13 only after the completion gate is satisfied.

## Visual Package

The dedicated diagrams are:

- [DIA-D00-065 — Reliability vs Availability vs Durability vs Resilience](../../../../docs/diagrams/D00/D00-T012/DIA-D00-065-reliability-availability-durability-resilience.md)
- [DIA-D00-066 — User Journey → Dependency Chain → Reliability Outcome](../../../../docs/diagrams/D00/D00-T012/DIA-D00-066-user-journey-dependency-reliability.md)
- [DIA-D00-067 — Failure Domain → Blast Radius → Redundancy Placement](../../../../docs/diagrams/D00/D00-T012/DIA-D00-067-failure-domain-blast-radius-redundancy.md)
- [DIA-D00-068 — Detect → Contain → Recover → Validate → Learn](../../../../docs/diagrams/D00/D00-T012/DIA-D00-068-detect-contain-recover-validate-learn.md)
- [DIA-D00-069 — SLI → SLO → Error Budget Mental Model](../../../../docs/diagrams/D00/D00-T012/DIA-D00-069-sli-slo-error-budget.md)
- [DIA-D00-070 — Capacity Headroom → Failure → Failover / Degradation](../../../../docs/diagrams/D00/D00-T012/DIA-D00-070-capacity-headroom-failure-recovery.md)

## Practical Package

- [OBS-D00-016 — Map a Critical User Journey and Reliability Boundaries](../../../../labs/observation/D00/OBS-D00-016-map-critical-user-journey-reliability-boundaries.md)
- [EXP-D00-019 — Reliability Targets, Failure Domains, Redundancy, and Graceful Degradation](../../../../labs/experiments/D00/EXP-D00-019-reliability-targets-failure-domains-degradation.md)
- [EXP-D00-020 — Recovery, Capacity Headroom, Backup Validation, and Incident Timeline](../../../../labs/experiments/D00/EXP-D00-020-recovery-capacity-backup-incident-timeline.md)

The practical assets remain **DRAFT** until they are completed end-to-end and promoted to `LAB-VERIFIED`.

## Assessment Package

The [D00-T012 Assessment Package](../../../../assessments/topics/D00/D00-T012/README.md) includes:

- 96-question knowledge check
- applied reliability-engineering scenario
- Senior/SRE/Architect follow-ups
- teach-back assessment
- scoring rubric
- remediation map

---

# 3. What Is Reliability?

Reliability is the ability of a system to deliver the expected service over time under expected operating conditions.

A practical model:

~~~text
Correct Service
+ Sufficient Availability
+ Acceptable Performance
+ Recoverability
+ Data Integrity
→ Reliable User Experience
~~~

Reliability is judged from the perspective of the service that users depend on.

Reliability targets should therefore be attached to important user and business flows rather than to whichever infrastructure metric is easiest to collect.

---

# 4. Reliability Is User-Centered

A database can be healthy while checkout is broken.

A cluster can be healthy while login is unavailable.

Therefore ask:

> Can the user complete the important action successfully?

This leads to critical-user-journey thinking.

---

# 5. Critical User Journey

A critical user journey is an end-to-end operation that matters to users or the business.

Examples:

- sign in
- checkout
- place an order
- publish a message
- complete a payment
- retrieve a critical record

Reliability should be tied to meaningful journeys, not only component health.

---

# 6. Availability

Availability asks:

> Is the service usable when needed?

Conceptually:

~~~text
Available Time
----------------
Total Relevant Time
~~~

But real service availability should be measured through user-relevant success criteria, not only machine uptime.

---

# 7. Reliability vs Availability

Availability is one dimension of reliability.

A service may be available but unreliable because:

- responses are incorrect
- latency is unacceptable
- data is stale beyond tolerance
- failures are frequent
- recovery is unstable

Reliability is broader.

---

# 8. Durability

Durability asks:

> Does committed data remain intact over time despite failures?

A service can be highly available but lose data.

A service can preserve data but be temporarily unavailable.

These are different properties.

---

# 9. Resilience

Resilience is the ability to absorb disruption, continue useful service where possible, and recover.

~~~text
Disturbance
→ Absorb
→ Degrade Safely
→ Recover
→ Learn
~~~

Resilience includes both technical and operational behavior.

---

# 10. Fault Tolerance

Fault tolerance means continuing correct or acceptable operation despite specific failures.

Examples may include:

- losing one node
- losing one replica
- losing one zone
- losing one dependency path

Fault tolerance is always relative to an explicit failure model.

---

# 11. Recoverability

Recoverability asks:

> After failure, how quickly and safely can the system return to acceptable service?

A system that cannot prevent every failure can still be highly reliable if it detects and recovers quickly.

---

# 12. Failure Model

A failure model defines what failures the system is designed to tolerate.

Examples:

- one process crash
- one node failure
- one availability-zone failure
- one database replica failure
- one dependency timeout
- one bad deployment

Without a defined failure model, "high availability" is vague.

---

# 13. Failure Domain

A failure domain is a boundary within which failures may be correlated.

Examples:

- process
- host
- rack
- zone
- region
- cluster
- database
- shared dependency

Redundancy only helps when redundant components do not fail together.

---

# 14. Blast Radius

Blast radius is the scope of impact caused by a failure.

A small blast radius may affect:

~~~text
one request
one replica
one tenant
~~~

A large blast radius may affect:

~~~text
one cluster
one region
all customers
~~~

Reliability engineering tries to limit correlated impact.

---

# 15. Redundancy

Redundancy adds extra components or capacity so one failure does not immediately remove service.

Examples:

- replicas
- multiple nodes
- multiple zones
- duplicate network paths
- backup systems

Redundancy is useful only if failures are sufficiently independent.

---

# 16. Redundancy Is Not Reliability by Itself

Three replicas on one failing host are not meaningfully independent.

Two databases using the same storage failure domain may fail together.

Therefore:

~~~text
Redundancy
+ Independence
+ Detection
+ Failover
+ Capacity
→ Useful Resilience
~~~

---

# 17. Graceful Degradation

Graceful degradation preserves critical functionality while reducing noncritical functionality.

Example:

~~~text
Recommendation Service Fails
→ Checkout Continues
→ Recommendations Hidden
~~~

This can preserve user-visible reliability.

---

# 18. Failover

Failover moves service to another healthy component or location after failure.

Conceptually:

~~~text
Primary Fails
→ Detect
→ Decide
→ Redirect / Promote
→ Validate
~~~

Failover itself can fail.

---

# 19. Active / Active — Preview

Multiple instances actively serve traffic.

Potential benefits:

- capacity
- redundancy
- faster failover

Potential challenges:

- state coordination
- traffic distribution
- consistency
- correlated dependencies

---

# 20. Active / Passive — Preview

One component serves traffic while another waits to take over.

Potential benefits:

- simpler write ownership
- clear failover role

Potential challenges:

- failover delay
- stale standby
- untested standby
- wasted capacity

Deep design comes later.

---

# 21. Recovery Is a System Feature

Recovery should not depend entirely on improvisation.

A mature recovery model considers:

~~~text
Detect
→ Diagnose
→ Contain
→ Restore
→ Validate
→ Learn
~~~

Recovery needs evidence, permissions, procedures, and practiced decisions.

---

# 22. Detection Time

A failure that begins at 10:00 but is noticed at 10:20 already consumed 20 minutes of user impact.

Detection time matters.

Fast recovery starts with fast, accurate detection.

---

# 23. Response Time

After detection, someone or something must decide what to do.

Poor alert context can delay response even when detection is fast.

Therefore alert quality affects reliability.

---

# 24. Recovery Time

Recovery time is how long it takes to restore acceptable service after failure.

Improving recovery often provides more value than trying to eliminate every possible failure.

---

# 25. MTTR — Mental Model

MTTR is commonly used to describe mean time to restore, recover, or repair, depending on context.

The exact definition must be stated before the metric is used or compared.

At D00 retain:

> Lower recovery time generally improves reliability, but averages can hide severe incidents.

Use percentiles/distributions where appropriate.

---

# 26. MTBF / MTTF — Preview

Metrics such as Mean Time Between Failures and Mean Time To Failure can be useful in some contexts.

But distributed software systems do not always fail like physical components.

Do not use these metrics mechanically.

---

# 27. SLI — Preview

A Service Level Indicator is a measured signal of service behavior.

Examples:

- successful request ratio
- latency
- availability
- freshness
- durability signal

The SLI should represent what users experience.

---

# 28. SLO — Preview

A Service Level Objective is a target for an SLI.

Conceptually:

~~~text
SLI
→ measured behavior

SLO
→ desired target
~~~

Example:

~~~text
99.9% successful requests over a defined window
~~~

Deep SLO engineering comes in the next SRE-focused topic.

---

# 29. SLA — Preview

A Service Level Agreement is a formal commitment, often with business or contractual consequences.

SLA is not the same as SLO.

A team may set internal SLOs tighter than external SLA commitments.

---

# 30. Error Budget — Preview

An error budget represents the amount of unreliability allowed by an SLO.

Conceptually:

~~~text
100% - SLO Target
→ allowed unreliability
~~~

The important operational lesson is that the budget should influence decisions about risk, change, and reliability work.

Detailed policy comes later.

---

# 31. Reliability Target

Not every service needs the same reliability.

A target should consider:

- user impact
- business criticality
- cost
- complexity
- recovery ability
- dependency limits

Higher reliability usually costs more.

---

# 32. Reliability vs Cost

Going from 99.9% to 99.99% can require disproportionate investment.

Potential costs include:

- redundancy
- multi-zone / multi-region design
- operational complexity
- more testing
- more observability
- more capacity
- more engineering time

Reliability is an engineering and business trade-off.

---

# 33. End-to-End Reliability

A frontend may be healthy while a payment provider fails.

A service may be healthy while DNS is broken.

Therefore reliability is end-to-end.

~~~text
User
→ DNS
→ Network
→ Load Balancer
→ App
→ Database
→ Queue
→ External Dependency
~~~

The weakest critical dependency can dominate the user journey.

---

# 34. Dependency Reliability

For each dependency ask:

- is it critical?
- is there a timeout?
- can we retry safely?
- can we degrade without it?
- can we cache?
- is there a fallback?
- what happens when it is slow rather than fully down?

Slow dependencies often create larger incidents than clean failures.

---

# 35. Reliability and Distributed Systems

Distributed systems fail partially.

Reliability engineering therefore asks:

~~~text
Which failures are expected?
How are they detected?
How are they contained?
How is service restored?
What trade-offs are acceptable?
~~~

---

# 36. Health Signals

A process being alive is not enough.

Useful health may include:

- readiness
- request success
- latency
- dependency health
- saturation
- queue depth
- data freshness

Health should align with the service objective.

---

# 37. Observability

Reliability depends on knowing what the system is doing.

Observability evidence includes:

- metrics
- logs
- traces
- events
- deployment markers
- dependency signals

Observability is not the same as reliability, but poor observability slows recovery.

---

# 38. Alert Quality

A useful alert should indicate something actionable.

Weak alert:

~~~text
CPU > 70%
~~~

Potentially stronger alert:

~~~text
Checkout error rate threatens SLO
and
database saturation is rising
~~~

Alerting should prioritize user impact and actionable symptoms.

---

# 39. Symptom vs Cause

A symptom is what users experience.

A cause is the underlying technical reason.

Example:

~~~text
Symptom
→ Checkout fails

Cause
→ Database connection pool exhausted
~~~

Reliability monitoring should detect symptoms quickly while troubleshooting identifies causes.

---

# 40. Change as Reliability Risk

Many incidents are triggered by change:

- deployment
- configuration update
- schema migration
- infrastructure change
- certificate rotation
- dependency upgrade

Safe change design is part of reliability engineering.

---

# 41. Small Changes Reduce Risk

Smaller changes are generally easier to:

- review
- validate
- understand
- roll back
- correlate with failure

This connects reliability to CI/CD and IaC.

---

# 42. Rollback vs Roll-Forward

Rollback returns to a previous version.

Roll-forward fixes the issue with a new version.

The correct choice depends on:

- data compatibility
- reversibility
- incident urgency
- known-good state
- deployment model

---

# 43. Capacity Headroom

A system running at nearly 100% capacity has little room for:

- traffic spikes
- node failure
- rescheduling
- retry load
- maintenance
- recovery

Reliability requires capacity for disturbance.

---

# 44. Saturation

Saturation means a resource is near or beyond useful capacity.

Examples:

- CPU
- memory
- connections
- queue depth
- threads
- disk I/O
- database sessions

Saturation often turns small problems into cascading failures.

---

# 45. Load Shedding

Under overload, rejecting some work can protect critical work.

~~~text
Demand > Safe Capacity
→ Drop / Reject Lower-Priority Work
→ Preserve Core Service
~~~

This is often more reliable than letting everything degrade slowly.

---

# 46. Backpressure

Backpressure prevents upstream producers from overwhelming downstream systems.

It helps convert uncontrolled overload into controlled flow.

---

# 47. Reliability and Queues

Queues can absorb bursts and decouple failures.

But sustained backlog means work is arriving faster than it can be processed.

Therefore monitor:

- depth
- age
- consumer rate
- retry volume
- dead-letter volume

---

# 48. Backup Is Not Recovery

A backup proves that data was copied.

Recovery requires proving that data can be restored correctly and within the required time and data-loss objectives.

Therefore:

~~~text
Backup
≠
Proven Recovery
~~~

Restore testing, validation, and measured recovery timing matter.

---

# 49. RTO — Preview

Recovery Time Objective asks:

> How quickly must service be restored after a serious disruption?

This is a business-driven recovery target.

---

# 50. RPO — Preview

Recovery Point Objective asks:

> How much recent data loss can be tolerated?

Examples:

~~~text
RPO = 0
→ no committed data loss tolerated

RPO = 15 min
→ up to 15 minutes may be acceptable
~~~

Deep disaster-recovery design comes later.

---

# 51. Disaster Recovery — Preview

Disaster recovery addresses major disruptions beyond routine local failures.

Examples:

- region loss
- major data corruption
- catastrophic infrastructure loss
- critical platform failure

DR is a subset of broader reliability planning.

---

# 52. Reliability Testing

Do not rely only on happy-path testing.

Reliability testing asks:

- what if dependency is slow?
- what if one node disappears?
- what if storage is unavailable?
- what if traffic doubles?
- what if a deployment is bad?
- what if recovery starts during peak load?

---

# 53. Failure Injection — Preview

Controlled failure testing can validate assumptions.

Examples conceptually:

- terminate one test replica
- simulate dependency unavailability
- simulate high latency
- simulate capacity loss

At D00 level, retain the principle:

> Test failure assumptions safely before production incidents test them for you.

Deep chaos engineering comes later.

---

# 54. Runbooks

A runbook captures known operational actions.

A good runbook may include:

- trigger
- symptoms
- checks
- decision points
- safe mitigation
- rollback/recovery
- validation
- escalation

Runbooks reduce cognitive load during incidents.

---

# 55. Incident Readiness

Reliability includes being ready for failure.

Questions:

- who owns the service?
- who can deploy?
- who can fail over?
- where are dashboards?
- where are logs?
- where is the runbook?
- who makes the decision?

Technology alone is not enough.

---

# 56. Human Reliability

Humans operate systems under stress.

Reliability improves when systems reduce:

- repetitive manual work
- unclear ownership
- dangerous access patterns
- ambiguous alerts
- undocumented recovery

Good system design reduces reliance on perfect human behavior.

---

# 57. Toil — Preview

Toil is repetitive operational work that scales with service growth and adds limited enduring value.

Examples:

- manual restarts
- repeated ticket handling
- recurring copy/paste fixes
- manual health checks

Automation can reduce toil, but automation must itself be reliable.

---

# 58. Production Readiness

Before launch, ask:

- failure modes known?
- dependencies understood?
- SLO/SLI defined?
- capacity sufficient?
- observability ready?
- backups/restores tested?
- recovery path known?
- rollback or roll-forward understood?
- on-call ownership clear?
- security controls ready?

Production readiness is a reliability gate.

---

# 59. Reliability Is Continuous

Reliability work does not stop after launch.

~~~text
Operate
→ Observe
→ Incident
→ Learn
→ Improve
→ Test Again
~~~

A reliable service evolves.

---

# 60. Common Beginner Mistakes

## Mistake 1

"Reliability means 100% uptime."

Absolute availability is usually unrealistic and costly.

## Mistake 2

"More replicas always means more reliability."

Replicas that share failure domains may fail together.

## Mistake 3

"Monitoring makes the system reliable."

Monitoring helps detection; it does not prevent or recover every failure.

## Mistake 4

"Backup means recovery is solved."

Untested restore procedures are not proven recovery.

## Mistake 5

"Failover is automatic, so we are safe."

Failover requires detection, capacity, correct state, and validation.

## Mistake 6

"High CPU means incident."

Reliability should focus on user impact and service objectives.

## Mistake 7

"We should eliminate all failures."

Better engineering often focuses on containment and fast recovery.

## Mistake 8

"Every service needs five-nines."

Reliability targets should match business value and cost.

---

# 61. Five-Level Explanation

## L1 — Foundation

Reliability means users can depend on a service to behave acceptably over time.

## L2 — Engineer

Reliable systems define failure modes, use redundancy, observe health, control change, preserve capacity, and recover from failure.

## L3 — Senior Engineer

Reliability engineering connects user journeys, failure domains, dependencies, detection, containment, recovery, capacity, deployment risk, and operational readiness.

## L4 — SRE

Reliability is managed through SLIs/SLOs, error budgets, alert quality, incident response, capacity, toil reduction, and measurable recovery behavior.

## L5 — Architect

Reliability architecture balances business targets, cost, redundancy, independence, consistency, failover, capacity, observability, recovery objectives, and organizational ownership.

---

# 62. Senior Engineer Perspective

A senior engineer asks:

- what user journey is failing?
- what changed?
- what is the failure domain?
- how large is the blast radius?
- what dependency is critical?
- is redundancy truly independent?
- is capacity sufficient for failover?
- can we degrade safely?
- what is the recovery path?
- how will we validate recovery?

---

# 63. SRE Perspective

An SRE asks:

- what SLI is affected?
- is the SLO at risk?
- how quickly did we detect the issue?
- what is the error-budget impact?
- is retry traffic worsening saturation?
- is capacity headroom sufficient?
- can we reduce blast radius?
- what is MTTR?
- what toil should be removed after the incident?

---

# 64. Architect Perspective

An architect asks:

- what reliability target does the business require?
- what failures must be tolerated?
- what redundancy is justified?
- what failure domains must be independent?
- what RTO/RPO are required?
- where is graceful degradation acceptable?
- what dependencies dominate reliability?
- what reliability cost is justified?
- what operational model supports recovery?

---

# 65. What You Must Retain

Before moving on, retain:

- reliability is broader than uptime
- availability, durability, resilience, fault tolerance, and recoverability are different
- reliability should be measured through user-relevant service
- critical user journeys matter more than isolated component health
- failure models make reliability claims meaningful
- redundancy helps only when failures are independent
- blast radius should be limited
- graceful degradation can preserve critical service
- failover requires detection, state, capacity, and validation
- recovery time is a design concern
- SLI, SLO, SLA, and error budget are different concepts
- reliability targets should match business value and cost
- dependency reliability is part of end-to-end reliability
- observability speeds detection and recovery
- alerts should be actionable and user-impact-aware
- change is a major reliability risk
- smaller changes reduce uncertainty
- rollback and roll-forward are different recovery strategies
- capacity headroom enables recovery
- saturation can trigger cascading failure
- load shedding and backpressure protect critical capacity
- backups do not prove recoverability
- RTO and RPO describe recovery expectations
- incident readiness includes ownership and procedures
- human factors and toil affect reliability
- production readiness is a reliability gate
- reliability is a continuous improvement process

---

# 66. Practical Package

Complete the practical assets:

1. [OBS-D00-016 — Map a Critical User Journey and Reliability Boundaries](../../../../labs/observation/D00/OBS-D00-016-map-critical-user-journey-reliability-boundaries.md)
2. [EXP-D00-019 — Reliability Targets, Failure Domains, Redundancy, and Graceful Degradation](../../../../labs/experiments/D00/EXP-D00-019-reliability-targets-failure-domains-degradation.md)
3. [EXP-D00-020 — Recovery, Capacity Headroom, Backup Validation, and Incident Timeline](../../../../labs/experiments/D00/EXP-D00-020-recovery-capacity-backup-incident-timeline.md)

These exercises turn reliability-engineering foundations into concrete reasoning around critical user journeys, reliability properties, failure domains, correlated redundancy, graceful degradation, SLI/SLO/SLA concepts, error budgets, failover assumptions, capacity headroom, saturation, alert quality, RTO/RPO, backup-vs-recovery, runbooks, and production readiness.

---

# 67. Assessment Package

Complete the [D00-T012 Assessment Package](../../../../assessments/topics/D00/D00-T012/README.md).

It tests:

- reliability vs availability
- durability, resilience, fault tolerance, and recoverability
- critical user journeys
- failure models, failure domains, and blast radius
- redundancy and independence
- graceful degradation
- failover
- detection, response, and recovery
- SLI, SLO, SLA, and error-budget concepts
- reliability/cost trade-offs
- dependency reliability
- observability and alert quality
- change risk
- rollback vs roll-forward
- capacity headroom and saturation
- load shedding and backpressure
- backup and recovery
- RTO and RPO
- incident readiness
- toil and human reliability
- production readiness
- Senior/SRE/Architect reasoning

---

# 68. Visual Package

Review the [D00-T012 Visual Package](../../../../docs/diagrams/D00/D00-T012/README.md).

The package includes:

1. Reliability vs Availability vs Durability vs Resilience
2. User Journey → Dependency Chain → Reliability Outcome
3. Failure Domain → Blast Radius → Redundancy Placement
4. Detect → Contain → Recover → Validate → Learn
5. SLI → SLO → Error Budget Mental Model
6. Capacity Headroom → Failure → Failover / Degradation

---

# 69. Completion Gate

Before moving on, confirm that you can:

- explain why reliability is broader than uptime
- distinguish availability, durability, resilience, fault tolerance, and recoverability
- define reliability from a critical user journey rather than component health
- explain why failure models make reliability claims meaningful
- identify failure domains and blast radius
- explain why redundancy requires independence
- explain graceful degradation and when it is safe
- explain failover as detect → decide → redirect/promote → validate
- explain why failover itself can fail
- distinguish active/active and active/passive at a high level
- explain detection time, response time, and recovery time separately
- explain why MTTR must be defined explicitly
- distinguish SLI, SLO, SLA, and error budget
- explain why 100% reliability is usually the wrong default target
- explain how reliability targets balance user need, cost, and complexity
- explain end-to-end dependency reliability
- distinguish health, observability, and reliability
- explain why user-impact-aware alerting is stronger than raw component thresholds alone
- distinguish symptom from root cause
- explain why change is a reliability risk
- compare rollback and roll-forward
- explain capacity headroom and why failover needs spare capacity
- explain saturation and cascading-failure risk
- explain load shedding and backpressure
- explain why queue backlog is a reliability signal
- explain why backup does not prove recovery
- distinguish RTO from RPO
- explain why restore/failover testing matters
- explain disaster recovery at the correct preview level
- explain why reliability testing must include failure scenarios
- explain runbook purpose and incident-readiness requirements
- explain how ownership, access, and human factors affect recovery
- explain toil at a high level
- explain why production readiness is a reliability gate
- complete the practical package
- score at least 80% on the knowledge check
- score at least 75% on the applied scenario
- demonstrate at least L3 / FD-3 reasoning
- teach the reliability-engineering mental model clearly without relying on notes

# 70. What Comes Next

After D00-T012 is completed, continue to:

## 00.13 — SRE Foundations

That topic will formalize service-level objectives, error budgets, toil, on-call, incident response, and reliability operating practices.

---

# 71. Sources & Evidence

Planned authoritative source families:

- Google SRE book and workbook
- Google Cloud reliability guidance
- AWS Well-Architected Reliability Pillar
- Azure Well-Architected Reliability guidance
- CNCF reliability / resilience material where useful
- disaster-recovery guidance from major cloud providers
- vendor-neutral reliability engineering references

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: authored as DRAFT; LAB-VERIFICATION pending
- assessment package: authored and cross-linked
- visual package: authored and cross-linked
- canonical learner journey: integrated

Detailed verification record:

- [D00-T012 Source Verification](../../../../docs/sources/D00/D00-T012-source-verification.md)

Verified nuances:

- reliability should be anchored to important user/business flows
- availability is one dimension of reliability, not the entire concept
- recoverability is part of reliability
- SLI, SLO, and SLA are different concepts and should not be used interchangeably
- 100% reliability is usually the wrong default target for software services
- error budgets represent allowed unreliability and should influence risk/change decisions
- reliability targets require business and engineering trade-offs
- change is a normal reliability input
- graceful degradation can preserve critical service when business correctness allows it
- redundancy is useful only when critical failure modes are sufficiently independent
- failover and recovery must be tested rather than assumed
- RTO and RPO answer different recovery questions
- MTTR is ambiguous unless its exact definition is stated
- monitoring, alert quality, access, runbooks, ownership, and validation all affect recovery time
- backup success alone does not prove recoverability
- capacity headroom supports failover, rescheduling, retries, maintenance, and recovery


## Topic Package Status

**D00-T012 is structurally complete.**

Remaining quality work is operational verification of the practical exercises. Once those exercises are completed and reviewed, their evidence status can be promoted from DRAFT to LAB-VERIFIED.
