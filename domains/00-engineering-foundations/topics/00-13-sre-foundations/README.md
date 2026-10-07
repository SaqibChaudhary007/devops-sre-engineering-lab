---
id: D00-T013
domain: D00
title: SRE Foundations
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
    - D00-T012
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
  - Think Like SRE
  - Architecture With Saqib
---

# 00.13 — SRE Foundations

## Start Here

You now understand reliability engineering at a systems level.

The next question is:

> How do we operate reliability as an engineering discipline with measurable objectives, controlled risk, automation, incident response, and continuous improvement?

That is the problem space of **Site Reliability Engineering (SRE)**.

SRE is not:

- monitoring only
- on-call only
- DevOps with a different title
- automation only
- incident response only
- "keeping production alive at any cost"
- zero change
- zero failure
- a replacement for software engineering

The core mental model is:

~~~text
User Need
→ SLI
→ SLO
→ Error Budget
→ Engineering Decision
→ Safe Change
→ Operate
→ Detect
→ Respond
→ Learn
→ Improve
~~~

SRE applies software-engineering methods to operations and reliability problems.

This D00 topic stays at the foundational mental-model level. Detailed SLO design, burn-rate alerting, incident command, toil measurement, on-call program design, reliability automation, and platform implementation come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- what SRE is
- why SRE exists
- SRE vs traditional operations
- SRE vs DevOps
- reliability as a product feature
- SLI
- SLO
- SLA
- error budget
- availability target
- latency target
- correctness target
- freshness target
- user journey
- service boundary
- error-budget policy
- change velocity
- risk management
- toil
- automation
- operational load
- on-call
- alerting
- symptoms vs causes
- paging vs ticketing
- incident response
- mitigation vs root-cause correction
- postmortems
- blameless learning
- capacity and saturation
- overload protection
- dependency reliability
- production readiness
- launch readiness
- ownership
- runbooks
- observability
- monitoring
- release engineering
- safe change
- rollback / roll-forward
- canary / progressive delivery preview
- reliability reviews
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
- [00.12 — Reliability Engineering Foundations](../00-12-reliability-engineering-foundations/README.md)

You should already understand user journeys, availability, recoverability, failure domains, blast radius, redundancy, capacity headroom, observability, SLI/SLO/error-budget previews, and incident recovery.

---

# Learning Package Navigation

Use this page as the canonical learner entry point.

Move through the package in this order:

1. **Learn** — complete the conceptual sections on this page.
2. **Verify** — review the [D00-T013 Source Verification](../../../../docs/sources/D00/D00-T013-source-verification.md).
3. **Visualize** — review the [D00-T013 Visual Package](../../../../docs/diagrams/D00/D00-T013/README.md).
4. **Observe SRE Objectives** — complete [OBS-D00-017 — Map a User Journey to SLI, SLO, and Alerting Decisions](../../../../labs/observation/D00/OBS-D00-017-user-journey-sli-slo-alerting.md).
5. **Experiment with Error Budgets & Toil** — complete [EXP-D00-021 — Error Budget, Toil, Automation, and Safe Change Decisions](../../../../labs/experiments/D00/EXP-D00-021-error-budget-toil-automation-safe-change.md).
6. **Experiment with Incidents & Readiness** — complete [EXP-D00-022 — Incident Response, Alert Actionability, Postmortem, and Production Readiness](../../../../labs/experiments/D00/EXP-D00-022-incident-alert-postmortem-production-readiness.md).
7. **Assess** — complete the [D00-T013 Assessment Package](../../../../assessments/topics/D00/D00-T013/README.md).
8. **Teach Back** — explain SRE at Beginner, Engineer, Senior, SRE, and Architect levels.
9. **Continue** — move to 00.14 only after the completion gate is satisfied.

## Visual Package

The dedicated diagrams are:

- [DIA-D00-071 — User Journey → SLI → SLO → Error Budget → Decision](../../../../docs/diagrams/D00/D00-T013/DIA-D00-071-user-journey-sli-slo-error-budget-decision.md)
- [DIA-D00-072 — Page vs Ticket vs Dashboard](../../../../docs/diagrams/D00/D00-T013/DIA-D00-072-page-ticket-dashboard.md)
- [DIA-D00-073 — Incident: Detect → Mitigate → Recover → Learn](../../../../docs/diagrams/D00/D00-T013/DIA-D00-073-incident-detect-mitigate-recover-learn.md)
- [DIA-D00-074 — Toil → Automation → Engineering Capacity](../../../../docs/diagrams/D00/D00-T013/DIA-D00-074-toil-automation-engineering-capacity.md)
- [DIA-D00-075 — Error Budget → Change Velocity / Reliability Trade-Off](../../../../docs/diagrams/D00/D00-T013/DIA-D00-075-error-budget-change-velocity-reliability.md)
- [DIA-D00-076 — Production Readiness → Operate → Incident → Improvement](../../../../docs/diagrams/D00/D00-T013/DIA-D00-076-production-readiness-operate-improve.md)

## Practical Package

- [OBS-D00-017 — Map a User Journey to SLI, SLO, and Alerting Decisions](../../../../labs/observation/D00/OBS-D00-017-user-journey-sli-slo-alerting.md)
- [EXP-D00-021 — Error Budget, Toil, Automation, and Safe Change Decisions](../../../../labs/experiments/D00/EXP-D00-021-error-budget-toil-automation-safe-change.md)
- [EXP-D00-022 — Incident Response, Alert Actionability, Postmortem, and Production Readiness](../../../../labs/experiments/D00/EXP-D00-022-incident-alert-postmortem-production-readiness.md)

The practical assets remain **DRAFT** until they are completed end-to-end and promoted to `LAB-VERIFIED`.

## Assessment Package

The [D00-T013 Assessment Package](../../../../assessments/topics/D00/D00-T013/README.md) includes:

- 96-question knowledge check
- applied SRE scenario
- Senior/SRE/Architect follow-ups
- teach-back assessment
- scoring rubric
- remediation map

---

# 3. What Is SRE?

SRE is an engineering approach to operating reliable services.

A practical mental model:

~~~text
Operations Problem
→ Measure It
→ Understand It
→ Automate Where Useful
→ Reduce Repetition
→ Control Risk
→ Improve Reliability
~~~

SRE treats operational work as an engineering problem rather than purely manual administration.

---

# 4. Why SRE Exists

Traditional operations can become dominated by:

- repetitive manual work
- reactive firefighting
- unclear reliability targets
- alert noise
- undocumented procedures
- fragile change processes
- scaling headcount with service growth

SRE tries to replace repeated operational effort with:

- software
- automation
- measurable objectives
- reliability policies
- better system design

---

# 5. SRE Is Not "No Operations"

Operations work still exists.

SRE asks:

> Which operational work should remain human judgment, and which should become engineered automation?

The goal is not to remove humans.

The goal is to use human attention where judgment matters most.

Operational work should be classified carefully: novel diagnosis and engineering work are not automatically toil simply because they happen in production.

---

# 6. SRE vs Traditional Operations

A simplified contrast:

~~~text
Traditional Operations
→ run tasks
→ follow procedures
→ respond manually

SRE
→ define objectives
→ measure behavior
→ engineer automation
→ reduce toil
→ improve system design
~~~

This is a mental model, not a claim that all operations teams work the same way.

---

# 7. SRE vs DevOps

DevOps is a broad set of cultural and engineering principles for improving software delivery and operations.

SRE is a concrete operating model focused on reliability.

A simple relationship:

~~~text
DevOps Principles
→ collaboration
→ fast feedback
→ automation
→ shared ownership

SRE Practices
→ SLOs
→ error budgets
→ toil control
→ on-call
→ incident learning
→ reliability engineering
~~~

They overlap heavily.

---

# 8. Reliability Is a Product Feature

Users do not care whether your internal systems look healthy.

They care whether the product works.

Therefore SRE begins with user-visible outcomes.

Examples:

- can users sign in?
- can users complete checkout?
- can messages be delivered?
- can orders be processed?
- is data fresh enough?

---

# 9. Service Boundary

Before measuring reliability, define the service boundary.

Ask:

- what service are we evaluating?
- which dependencies belong inside the boundary?
- which external dependencies influence the outcome?
- what user journey represents success?

Poorly defined boundaries create misleading reliability metrics.

---

# 10. SLI

A Service Level Indicator is a measured signal of service behavior.

Examples:

- request success ratio
- latency
- freshness
- availability
- durability signal
- throughput where relevant

The best SLI reflects what the user experiences.

---

# 11. SLO

A Service Level Objective is a target for an SLI over a defined period.

Example:

~~~text
SLI
→ successful checkout ratio

SLO
→ 99.9% successful checkouts over 30 days
~~~

The SLO tells the team what level of reliability is expected.

---

# 12. SLA

A Service Level Agreement is a formal commitment, often with customer or business consequences.

SLA is not the same as SLO.

Teams may intentionally set internal SLOs tighter than external commitments.

---

# 13. Error Budget

An error budget represents the allowed unreliability implied by an SLO.

Conceptually:

~~~text
100% - SLO
→ Allowed Unreliability
~~~

For:

~~~text
SLO = 99.9%
~~~

the conceptual error budget is:

~~~text
0.1%
~~~

The more important lesson is how that budget affects decisions.

---

# 14. Why Error Budgets Matter

Without a shared reliability target:

~~~text
Product Team
→ wants faster change

Reliability Team
→ wants fewer failures
~~~

This can become a permanent argument.

Error-budget thinking creates a shared decision framework around acceptable risk.

The exact response to budget consumption belongs to an explicit organizational policy; one company's freeze or escalation rule should not be treated as a universal SRE standard.

---

# 15. Error Budget as a Control Signal

When reliability is healthy:

~~~text
Budget Healthy
→ More Change Can Be Acceptable
~~~

When reliability is poor:

~~~text
Budget Burning Too Fast
→ Reduce Risk
→ Investigate
→ Improve Reliability
~~~

This is a policy concept, not a universal automatic rule.

---

# 16. 100% Reliability Is Usually the Wrong Goal

A 100% target often implies:

- extreme cost
- slower change
- unnecessary complexity
- unrealistic operational expectations

SRE aims for the **right** reliability level, not maximum reliability at any cost.

---

# 17. Availability SLI

An availability SLI might measure:

~~~text
Good Requests
-------------
Valid Requests
~~~

The exact definition depends on the service.

The important question is:

> What counts as "good" from the user's perspective?

---

# 18. Latency SLI

A request can succeed but still be too slow.

Therefore latency often belongs in reliability.

Example:

~~~text
99% of successful checkout requests
complete under 2 seconds
~~~

Averages are usually weaker than percentile/threshold-based thinking.

---

# 19. Correctness SLI

A response can be fast and available but wrong.

Examples:

- duplicate order
- incorrect balance
- wrong entitlement
- stale configuration

Some services need correctness-oriented indicators.

---

# 20. Freshness SLI

For systems where data timeliness matters:

~~~text
How fresh is the data?
~~~

Examples:

- monitoring dashboards
- replication feeds
- analytics pipelines
- inventory status

Freshness can be a reliability dimension.

---

# 21. User Journey First

A strong SRE sequence is:

~~~text
User Journey
→ Success Definition
→ SLI
→ SLO
→ Alert
→ Operational Decision
~~~

Not:

~~~text
Metric Exists
→ Create Alert
→ Call It Reliability
~~~

---

# 22. Symptoms vs Causes

Symptom:

~~~text
Users cannot check out
~~~

Cause:

~~~text
Database pool exhausted
~~~

SRE monitoring should prioritize user-impact symptoms while diagnostics help find causes.

---

# 23. Monitoring vs Observability

Monitoring asks:

> Are known important things behaving as expected?

Observability helps answer:

> Why is the system behaving this way?

SRE needs both.

---

# 24. Paging vs Ticketing

Not every problem deserves immediate human interruption.

A mental model:

~~~text
Page
→ urgent, actionable, user-impacting

Ticket
→ important but not immediately urgent

Dashboard
→ context and investigation
~~~

Poor paging policy creates alert fatigue.

---

# 25. A Good Page

A strong page should be:

- urgent
- actionable
- tied to user/service impact
- specific enough to start investigation

Organizations can use different tools and names, but the decision principle remains urgency plus actionability.

A weak page often reports:

~~~text
CPU = 81%
~~~

without explaining whether users are affected.

---

# 26. Alert Fatigue

Too many noisy alerts cause:

- slower response
- ignored pages
- burnout
- missed real incidents

Reducing noise is a reliability improvement.

---

# 27. On-Call

On-call means someone is responsible for responding to urgent service-impacting events.

A sustainable on-call system needs:

- clear ownership
- actionable alerts
- access
- runbooks
- escalation
- manageable load
- recovery support

---

# 28. On-Call Is a Product Feedback Loop

On-call pain is evidence.

Repeated incidents may reveal:

- missing automation
- poor architecture
- weak observability
- bad alerts
- fragile dependencies
- excessive toil

A mature SRE team converts pain into engineering work.

---

# 29. Toil

Toil is operational work that is repetitive, manual, automatable, tactical, and scales with service growth while providing limited enduring value.

Examples:

- repeated restarts
- manual ticket processing
- repeated health checks
- recurring copy/paste fixes
- manual deployment repair

Not every operational task is toil.

Toil is best recognized through characteristics such as manual effort, repetition, automability, tactical/reactive nature, limited enduring value, and growth with service scale.

---

# 30. Toil Is a Scaling Problem

If:

~~~text
Service Growth
→ More Manual Work
→ More People Needed
~~~

the operating model may not scale.

SRE tries to reduce this slope through engineering.

---

# 31. Automation

Automation should remove repeated, understood work.

Good automation usually follows:

~~~text
Understand Task
→ Define Safe Conditions
→ Automate
→ Observe
→ Validate
→ Improve
~~~

Automating a poorly understood process can make failures faster.

---

# 32. Human Judgment vs Automation

Not every decision should be automated.

Human judgment is often valuable when:

- impact is unclear
- trade-offs are unusual
- business context matters
- irreversible actions are possible

SRE balances automation with safe decision boundaries.

---

# 33. Incident

An incident is an event that significantly disrupts expected service or threatens reliability objectives.

Incidents vary by severity.

Not every alert is an incident.

---

# 34. Incident Response Goal

The first priority is usually:

~~~text
Reduce User Impact
~~~

not:

~~~text
Immediately Find the Perfect Root Cause
~~~

Mitigation and diagnosis are related but different.

---

# 35. Mitigation vs Root-Cause Fix

Mitigation:

~~~text
Restore Acceptable Service
~~~

Root-cause correction:

~~~text
Remove / Reduce Underlying Cause
~~~

During an incident, safe mitigation may come first.

---

# 36. Incident Timeline

A useful incident timeline may include:

~~~text
Failure Starts
→ Detection
→ Triage
→ Mitigation
→ Recovery
→ Validation
→ Learning
~~~

This helps identify where time was lost.

---

# 37. Incident Roles — Preview

Larger incidents may need clear roles such as:

- incident commander
- operations lead
- communications lead
- subject-matter experts

Detailed incident command comes later.

---

# 38. Postmortem

A postmortem captures what happened, impact, contributing factors, response, and improvements.

The goal is learning.

Blameless learning does not mean accountability-free operation. It means examining the system, information, tooling, incentives, and context that shaped decisions so recurrence risk can be reduced.

A strong postmortem asks:

- what conditions made this incident possible?
- why was impact large?
- why did detection take this long?
- why did recovery take this long?
- what systemic changes reduce recurrence?

---

# 39. Blameless Learning

Blameless learning does not mean ignoring mistakes.

It means examining how systems, incentives, tools, procedures, and context shaped human decisions.

The goal is safer systems, not fear-driven reporting.

---

# 40. Reliability Action Items

Good postmortem actions should be:

- specific
- owned
- prioritized
- trackable
- connected to risk reduction

"We should be more careful" is not a strong engineering action item.

---

# 41. Release Engineering

Reliable delivery requires changes to be:

- repeatable
- observable
- reversible where possible
- validated
- small enough to reason about

SRE therefore connects strongly to CI/CD.

---

# 42. Safe Change

A safe-change mental model:

~~~text
Small Change
→ Automated Checks
→ Progressive Exposure
→ Observe
→ Validate
→ Continue / Stop / Recover
~~~

Deep rollout strategies come later.

---

# 43. Canary / Progressive Delivery — Preview

Instead of exposing all users immediately:

~~~text
Small Audience
→ Observe
→ Expand Gradually
~~~

This can reduce initial blast radius.

It does not prove correctness and does not eliminate the need for representative traffic, meaningful telemetry, evaluation thresholds, sufficient observation time, stop/rollback capability, or correctness checks.

---

# 44. Rollback vs Roll-Forward

Rollback returns to a previous known-good state.

Roll-forward applies a corrective change.

The right choice depends on:

- reversibility
- schema compatibility
- data mutation
- incident urgency
- confidence

---

# 45. Capacity Is Part of Reliability

A service can be logically correct but unreliable under load.

SRE therefore watches:

- utilization
- saturation
- queue depth
- latency
- throughput
- headroom
- dependency capacity

---

# 46. Capacity Headroom

Headroom supports:

- traffic spikes
- node loss
- rescheduling
- retry traffic
- maintenance
- failover

A system with no headroom is fragile.

---

# 47. Overload Protection

When demand exceeds safe capacity, reliability may require:

- load shedding
- backpressure
- admission control
- retry limiting
- graceful degradation
- prioritization

Serving fewer requests well can be safer than serving all requests badly.

---

# 48. Dependency Reliability

A service inherits risk from dependencies.

Ask:

- what if dependency is down?
- what if it is slow?
- can we degrade?
- can we cache?
- can we retry safely?
- can we isolate failure?
- does the dependency have its own SLO?

---

# 49. Production Readiness

Before launch, SRE asks whether a service is ready to be operated.

Questions include:

- SLI/SLO defined?
- critical dependencies known?
- dashboards ready?
- alerts actionable?
- capacity understood?
- recovery tested?
- runbook available?
- ownership clear?
- change process safe?

---

# 50. Launch Readiness

A service can be technically functional but operationally unready.

Launch readiness is about whether the team can:

~~~text
Observe
→ Detect
→ Respond
→ Recover
→ Learn
~~~

after the service reaches users.

---

# 51. Ownership

Reliable services need clear ownership.

Ownership answers:

- who changes the service?
- who responds to incidents?
- who approves risky changes?
- who maintains runbooks?
- who owns SLOs?
- who follows up on reliability work?

---

# 52. Reliability Review

A reliability review can ask:

- what changed?
- what failed?
- what consumed error budget?
- what recurring toil exists?
- what incidents repeated?
- where is capacity weak?
- which action items remain open?

Reliability should be reviewed continuously.

---

# 53. SRE Is Not "Block All Change"

A reliability organization that blocks all change may reduce short-term risk but create:

- outdated systems
- delayed fixes
- operational friction
- slower learning

SRE aims for **safe velocity**, not zero velocity.

---

# 54. SRE Is Risk Management

SRE does not try to eliminate all risk.

It asks:

~~~text
What risk is acceptable?
How do we measure it?
How do we detect when it is too high?
What do we change when reliability degrades?
~~~

This is why SLOs and error budgets matter.

---

# 55. Common Beginner Mistakes

## Mistake 1

"SRE is monitoring."

Monitoring is one input. SRE is a broader reliability operating model.

## Mistake 2

"SRE means 100% uptime."

SRE uses explicit reliability targets and accepts bounded unreliability.

## Mistake 3

"Every alert should page."

Only urgent, actionable, user-impacting conditions should generally interrupt humans immediately.

## Mistake 4

"More automation always improves reliability."

Unsafe automation can increase blast radius.

## Mistake 5

"On-call means firefighting."

On-call should generate engineering feedback that reduces repeated incidents.

## Mistake 6

"Postmortem means finding who made the mistake."

Postmortems should identify systemic contributing factors and improvements.

## Mistake 7

"Error budget means permission to be careless."

An error budget is a risk-management mechanism, not permission for negligent change.

## Mistake 8

"Reliability work slows product development."

Good reliability engineering can increase sustainable delivery speed by reducing instability and firefighting.

---

# 56. Five-Level Explanation

## L1 — Foundation

SRE uses engineering methods to keep services reliably useful for users.

## L2 — Engineer

SRE measures reliability with SLIs/SLOs, uses error budgets to manage risk, improves monitoring, automates repetitive operations, and prepares for incidents.

## L3 — Senior Engineer

SRE connects user journeys, service boundaries, alerts, on-call, toil, dependencies, capacity, change safety, mitigation, and recovery.

## L4 — SRE

SRE operates reliability through SLOs, error budgets, sustainable on-call, incident response, production readiness, toil reduction, release safety, and continuous reliability improvement.

## L5 — Architect

SRE architecture balances product velocity, reliability targets, cost, risk, dependency design, capacity, operational ownership, and organization-wide reliability practices.

---

# 57. Senior Engineer Perspective

A senior engineer asks:

- what user journey is affected?
- what SLI represents that journey?
- what changed?
- is the alert actionable?
- is retry traffic worsening the problem?
- is there enough capacity?
- can we degrade safely?
- what is the fastest safe mitigation?
- what evidence proves recovery?

---

# 58. SRE Perspective

An SRE asks:

- what SLO is at risk?
- how much error budget is being consumed?
- should this condition page?
- what toil does this incident expose?
- what automation is justified?
- is on-call load sustainable?
- what recurring failure should become engineering work?
- what reliability action should be prioritized?

---

# 59. Architect Perspective

An architect asks:

- what reliability target is justified?
- where should SRE ownership live?
- which services need explicit SLOs?
- how should error-budget policy influence change?
- what dependencies dominate risk?
- how should systems degrade?
- what organizational model sustains on-call?
- what automation reduces systemic toil?
- what reliability cost is justified?

---

# 60. What You Must Retain

Before moving on, retain:

- SRE is an engineering approach to operations and reliability
- SRE is not monitoring only
- SRE is not identical to DevOps
- reliability begins with user journeys
- service boundaries matter
- SLI, SLO, SLA, and error budget are distinct
- error budgets help manage reliability vs change velocity
- 100% reliability is usually the wrong default
- symptoms should drive user-impact awareness
- observability supports diagnosis
- not every alert should page
- pages should be actionable and urgent
- on-call should feed engineering improvement
- toil is a scaling problem
- automation should follow understanding
- mitigation and root-cause correction are different
- incident timelines reveal response delays
- postmortems should drive systemic improvement
- blameless does not mean accountability-free
- release engineering is part of reliability
- progressive exposure can reduce blast radius
- capacity headroom supports recovery
- overload protection is part of reliability
- dependency reliability is end-to-end reliability
- production readiness includes operational readiness
- ownership must be explicit
- SRE aims for safe velocity, not zero change
- SRE is fundamentally risk management

---

# 61. Practical Package

Complete the practical assets:

1. [OBS-D00-017 — Map a User Journey to SLI, SLO, and Alerting Decisions](../../../../labs/observation/D00/OBS-D00-017-user-journey-sli-slo-alerting.md)
2. [EXP-D00-021 — Error Budget, Toil, Automation, and Safe Change Decisions](../../../../labs/experiments/D00/EXP-D00-021-error-budget-toil-automation-safe-change.md)
3. [EXP-D00-022 — Incident Response, Alert Actionability, Postmortem, and Production Readiness](../../../../labs/experiments/D00/EXP-D00-022-incident-alert-postmortem-production-readiness.md)

These exercises turn SRE foundations into concrete reasoning around service boundaries, SLI/SLO/SLA, error budgets, page/ticket/dashboard decisions, toil, automation safety, on-call feedback, incident response, mitigation, recovery validation, postmortem learning, progressive delivery, and production readiness.

---

# 62. Assessment Package

Complete the [D00-T013 Assessment Package](../../../../assessments/topics/D00/D00-T013/README.md).

It tests:

- SRE definition and purpose
- SRE vs DevOps / operations
- service boundaries
- SLI / SLO / SLA
- error budgets
- page vs ticket
- alert quality
- on-call
- toil
- automation
- incident response
- mitigation vs root cause
- postmortems
- blameless learning
- release engineering
- safe change
- capacity and headroom
- overload protection
- dependency reliability
- production readiness
- ownership
- reliability reviews
- risk management
- Senior/SRE/Architect reasoning

---

# 63. Visual Package

Review the [D00-T013 Visual Package](../../../../docs/diagrams/D00/D00-T013/README.md).

The package includes:

1. User Journey → SLI → SLO → Error Budget → Decision
2. Page vs Ticket vs Dashboard
3. Incident: Detect → Mitigate → Recover → Learn
4. Toil → Automation → Engineering Capacity
5. Error Budget → Change Velocity / Reliability Trade-Off
6. Production Readiness → Operate → Incident → Improvement

---

# 64. Completion Gate

Before moving on, confirm that you can:

- explain what SRE is and why it exists
- explain why SRE is broader than monitoring or on-call
- explain the relationship between SRE and DevOps without forcing a false hard boundary
- define a service boundary
- map a critical user journey to a good-event definition
- distinguish SLI, SLO, SLA, and error budget
- explain availability, latency, correctness, and freshness as possible reliability indicators
- explain why 100% reliability is usually the wrong default target
- explain how error-budget health can influence change/risk decisions
- explain why one organization's error-budget policy is not universal
- distinguish page, ticket, and dashboard/context decisions
- explain urgency and actionability
- distinguish symptoms from causes
- explain sustainable on-call
- explain how on-call pain becomes engineering feedback
- define toil and distinguish it from novel diagnosis or engineering work
- explain why toil is a scaling problem
- explain why automation should follow understanding and safety boundaries
- explain when human judgment should remain involved
- distinguish an incident from an alert
- distinguish mitigation from permanent/root-cause correction
- build an incident timeline
- explain why recovery must be validated against the user journey
- explain the purpose of postmortems
- explain blameless systemic learning without removing accountability
- design specific, owned, trackable reliability action items
- explain why release engineering is part of reliability
- explain progressive/canary delivery at the correct preview level
- explain why a canary reduces exposure but does not prove correctness
- compare rollback and roll-forward
- explain capacity headroom and overload protection
- explain dependency reliability as part of end-to-end service reliability
- explain production and launch readiness
- explain why ownership must be explicit
- explain reliability reviews as a continuous operating practice
- explain why SRE aims for safe velocity rather than zero change
- explain SRE as risk management
- complete the practical package
- score at least 80% on the knowledge check
- score at least 75% on the applied scenario
- demonstrate at least L3 / FD-3 reasoning
- teach the SRE mental model clearly without relying on notes

# 65. What Comes Next

After D00-T013 is completed, continue to:

## 00.14 — Observability Foundations

That topic will deepen metrics, logs, traces, events, telemetry design, signal quality, context, correlation, and troubleshooting evidence.

---

# 66. Sources & Evidence

Planned authoritative source families:

- Google SRE book
- Google SRE workbook
- Google Cloud SRE guidance
- AWS reliability and operational excellence guidance
- Azure Well-Architected reliability guidance
- CNCF observability/reliability material where useful
- vendor-neutral incident-management references

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: authored as DRAFT; LAB-VERIFICATION pending
- assessment package: authored and cross-linked
- visual package: authored and cross-linked
- canonical learner journey: integrated

Detailed verification record:

- [D00-T013 Source Verification](../../../../docs/sources/D00/D00-T013-source-verification.md)

Verified nuances:

- SRE is an engineering operating model, not merely monitoring, on-call, or tooling
- DevOps and SRE overlap heavily but should not be taught as identical or as mutually exclusive categories
- SLIs and SLOs should follow user/service needs rather than arbitrary available metrics
- 100% reliability is usually the wrong default target
- error budgets are decision mechanisms whose consequences depend on explicit organizational policy
- Google's specific operational thresholds and freeze rules are examples, not universal SRE standards
- toil is multi-dimensional and not every operational task is toil
- automation should follow understanding and safe conditions
- page/ticket/dashboard is a decision model based on urgency and actionability, not a mandatory tooling taxonomy
- on-call should feed engineering improvement rather than permanent firefighting
- mitigation and root-cause correction are different phases
- blameless learning is systemic but not accountability-free
- canarying/progressive delivery reduces exposure but does not prove correctness
- capacity/headroom and overload control belong to reliability operations
- production readiness includes operational readiness, ownership, observability, recovery, and safe change


## Topic Package Status

**D00-T013 is structurally complete.**

Remaining quality work is operational verification of the practical exercises. Once those exercises are completed and reviewed, their evidence status can be promoted from DRAFT to LAB-VERIFIED.
