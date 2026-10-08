---
id: D00-T018
domain: D00
title: Failure Thinking
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
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
    - D00-T013
    - D00-T014
    - D00-T015
    - D00-T016
    - D00-T017
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - Why Does It Exist
  - How It Really Works
  - Under the Hood
  - Build Break Fix
  - Production Room
  - Think Like SRE
  - Architecture With Saqib
  - Five Levels
---

# 00.18 — Failure Thinking

## Start Here

You now understand systems as interacting components with constraints, feedback loops, delays, shared dependencies, and global outcomes.

The next question is:

> What happens when one or more assumptions stop being true, and how should we design, operate, and recover when failure is normal rather than exceptional?

That is the problem space of **failure thinking**.

Failure thinking is not:

- expecting everything to break all the time
- assuming one root cause explains every incident
- adding retries everywhere
- adding replicas and calling the system resilient
- waiting for production incidents to discover failure modes
- deliberately damaging real systems without safeguards
- treating only complete outages as failures
- assuming slow, stale, partial, or ambiguous behavior is healthy
- believing redundancy automatically removes risk

The core mental model is:

~~~text
Assumption
→ Fault / Stressor
→ Error / Degraded State
→ Failure Mode
→ User / System Impact
→ Detection
→ Containment
→ Recovery
→ Validation
→ Learning
~~~

A second useful model is:

~~~text
What Can Fail?
→ How Will It Fail?
→ How Will Failure Propagate?
→ How Will We Detect It?
→ How Will We Limit Impact?
→ How Will We Recover?
→ How Will We Prove Recovery?
~~~

Failure thinking turns architecture from:

~~~text
"How does this work when everything is healthy?"
~~~

into:

~~~text
"How does this behave when dependencies are slow, state is uncertain, capacity is exhausted, changes are wrong, and only part of the system succeeds?"
~~~

This D00 topic stays at the foundational mental-model level. Formal fault-tree analysis, FMEA, chaos-engineering tooling, distributed-consensus proofs, quorum mathematics, advanced disaster recovery, formal verification, and platform-specific resilience patterns belong to later domains.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- fault
- error
- failure
- failure mode
- impact
- failure domain
- fault domain
- blast radius
- transient failure
- intermittent failure
- permanent failure
- partial failure
- correlated failure
- common-mode failure
- dependency failure
- gray / partial degradation
- slow failure
- stale-data failure
- overload
- saturation
- resource exhaustion
- cascading failure
- failure propagation
- hidden / latent failure
- fail-fast behavior
- retries and retry amplification
- timeout boundaries
- graceful degradation
- load shedding
- backpressure
- isolation / bulkhead preview
- circuit-breaker preview
- redundancy
- independence
- failover
- failback preview
- active / passive preview
- recovery
- recovery validation
- rollback
- roll-forward
- compensating action
- data recovery
- backup vs restore
- RTO / RPO preview
- network partition preview
- split-brain preview
- quorum preview
- state uncertainty
- duplicate processing
- idempotency connection
- change failure
- configuration failure
- security-control failure
- human / process failure
- observability failure
- detection gaps
- alerting failure
- runbook failure
- control-plane vs data-plane failure
- failure testing
- fault injection preview
- game days
- chaos engineering preview
- pre-mortem thinking
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
- [00.12 — Reliability Engineering Foundations](../00-12-reliability-engineering-foundations/README.md)
- [00.13 — SRE Foundations](../00-13-sre-foundations/README.md)
- [00.14 — Observability Foundations](../00-14-observability-foundations/README.md)
- [00.15 — Security Foundations](../00-15-security-foundations/README.md)
- [00.16 — Automation Mental Models](../00-16-automation-mental-models/README.md)
- [00.17 — Systems Thinking](../00-17-systems-thinking/README.md)

You should already understand distributed dependencies, queues, retries, saturation, feedback loops, observability, blast radius, SLOs, automation guardrails, and systems thinking.

---

# 3. What Is Failure Thinking?

Failure thinking means designing and operating systems with explicit assumptions about what can go wrong.

It asks:

~~~text
Healthy Path?
Failure Path?
Degraded Path?
Recovery Path?
~~~

The goal is not pessimism.

The goal is to make failure understandable, bounded, detectable, recoverable, and learnable.

---

# 4. Fault, Error, and Failure

A useful conceptual chain is:

~~~text
Fault
→ Error / Incorrect Internal State
→ Failure / Incorrect Externally Visible Behavior
~~~

Example:

~~~text
Fault:
dependency becomes unavailable

Error:
request handler cannot obtain required response

Failure:
checkout request fails for user
~~~

Terminology can vary across reliability, safety, and distributed-systems traditions, so focus on the conceptual relationship rather than overfitting to one formal vocabulary.

---

# 5. Failure Mode

A failure mode describes **how** something fails.

Examples:

- unavailable
- slow
- returns errors
- returns stale data
- returns incorrect data
- accepts work but never completes it
- completes twice
- loses state
- becomes partially reachable

"Service failed" is often too vague.

---

# 6. Impact

Failure becomes operationally meaningful when it affects:

- users
- data
- business outcomes
- security
- availability
- recovery
- dependent systems

Always connect:

~~~text
Failure Mode
→ Observable Impact
~~~

---

# 7. Failure Domain

A failure domain is a scope within which failures can be correlated.

Examples:

- process
- host
- node
- rack
- zone
- region
- account/project
- database cluster
- shared identity
- deployment pipeline

Design should ask whether supposedly redundant components really occupy independent failure domains.

---

# 8. Blast Radius

Blast radius asks:

> If this fails, how much can it affect?

Possible scopes:

~~~text
One Request
One Pod
One Service
One Tenant
One Zone
One Region
Whole Platform
~~~

Good architecture tries to keep failure local.

---

# 9. Transient Failure

A transient failure is temporary.

Examples conceptually:

- brief network interruption
- short dependency overload
- temporary lock contention
- momentary rate limit

Retries may help when repetition is safe, the failure is plausibly transient, the attempt count is bounded, and the dependency is not being further overloaded.

---

# 10. Permanent Failure

A permanent failure does not disappear simply by waiting.

Examples:

- invalid configuration
- revoked permission
- missing required resource
- incompatible schema
- corrupt artifact

Blind retries waste time and may amplify load.

---

# 11. Intermittent Failure

An intermittent failure appears and disappears.

It can be difficult to diagnose because:

- evidence is inconsistent
- timing matters
- symptoms may vanish before investigation

Good telemetry and timelines matter.

---

# 12. Partial Failure

Distributed systems often fail partially.

Example:

~~~text
API healthy
Database healthy
Payment dependency degraded
Queue healthy
One region degraded
~~~

"System up" or "system down" is often too simple.

---

# 13. Gray Failure

A gray failure is a condition where some observers see the system as healthy while others experience failure.

Examples:

- health check passes but user requests fail
- one network path works, another does not
- one region succeeds, another times out
- service is reachable but extremely slow

Gray failures are dangerous because different observers can disagree about whether the system is healthy.

At D00, treat "gray failure" as a useful mental model for observer-dependent or partial degradation rather than as one universally standardized formal definition.

---

# 14. Slow Is a Failure Mode

A dependency does not need to be completely down to cause failure.

~~~text
Dependency Slows
→ Threads / Connections Wait
→ Queues Grow
→ Timeouts Rise
→ Retries Rise
→ System Saturates
~~~

Latency can be a failure signal.

---

# 15. Stale Data as Failure

A service can be available but return stale information.

Depending on the system, stale data may be:

- acceptable
- degraded
- dangerous
- business-invalid

Correctness and freshness can matter as much as availability.

---

# 16. Incorrect Data as Failure

A fast successful response with incorrect data can be worse than an explicit error.

Reliability must include:

- correctness
- integrity
- freshness
- completeness

where those properties matter.

---

# 17. Dependency Failure

A service can be healthy internally but fail because a dependency is unavailable, slow, overloaded, or incorrect.

Ask:

- is the dependency required?
- can we degrade?
- can we cache?
- can we queue?
- can we fail fast?
- can we continue partially?

---

# 18. Dependency Chain Failure

A user outcome may depend on:

~~~text
DNS
→ Network
→ API
→ Auth
→ Database
→ Payment
→ Queue
~~~

Failure probability and latency accumulate across the chain.

End-to-end reliability belongs to the journey, not one component.

---

# 19. Correlated Failure

Failures are correlated when the same condition affects multiple supposedly separate components.

Examples:

- same zone
- same database
- same cloud account
- same IAM quota
- same certificate
- same deployment
- same operator action

Correlation defeats naive redundancy.

---

# 20. Common-Mode Failure

A common-mode failure causes multiple redundant paths to fail for the same underlying reason.

Example:

~~~text
Replica A
Replica B
Replica C
but
all depend on same database
~~~

Redundancy without independence can create false confidence.

---

# 21. Hidden Shared Dependency

A failure domain may be hidden.

Examples:

- shared DNS
- shared secrets system
- shared control plane
- shared artifact registry
- shared CI/CD runner
- shared human approval queue

Architecture diagrams should search for hidden dependencies.

---

# 22. Overload Failure

Overload occurs when demand exceeds safe capacity.

Symptoms may include:

- rising latency
- queue growth
- timeouts
- connection exhaustion
- retries
- dropped work
- partial unavailability

Overload is often a system feedback problem.

---

# 23. Resource Exhaustion

Failures can result from exhausted:

- CPU
- memory
- disk
- file descriptors
- threads
- connections
- queue capacity
- API quota
- human attention

Resources are not only compute resources.

---

# 24. Cascading Failure

A cascading failure spreads.

Example:

~~~text
Dependency Slows
→ Request Latency
→ Retries
→ Connection Growth
→ Queue Growth
→ More Saturation
→ Wider Failure
~~~

Containment should interrupt propagation.

---

# 25. Failure Propagation

Ask:

~~~text
Where Can Failure Travel?
~~~

Propagation paths include:

- synchronous dependency calls
- retries
- shared resource pools
- shared credentials
- queues
- deployment systems
- data corruption
- human actions

---

# 26. Failure Amplification

A small failure can become large because of:

- retries
- fan-out
- synchronized clients
- unbounded queues
- shared resource contention
- aggressive autoscaling
- broad automation

Systems should be designed to damp rather than amplify failure.

---

# 27. Timeout Boundary

A timeout bounds waiting.

Without it:

~~~text
Dependency Slow
→ Caller Waits
→ Resources Remain Occupied
→ Saturation Spreads
~~~

Timeouts should reflect the end-to-end time budget.

---

# 28. Fail Fast

Fail-fast behavior stops waiting or processing when success is no longer likely or useful.

This can protect:

- resources
- latency budgets
- dependencies
- recovery time

Fail-fast does not mean careless rejection; it should be tied to known conditions.

---

# 29. Retry Connection

Retries can recover transient faults.

But they can also:

- repeat side effects
- increase dependency load
- consume latency budget
- create retry storms

Retry safety was introduced in D00-T016 and becomes a failure-propagation concern here.

---

# 30. Backoff and Jitter Connection

Backoff reduces retry pressure.

Jitter reduces synchronization.

Conceptually:

~~~text
Failure
→ Wait
→ Retry Less Aggressively
→ Avoid Retry Herd
~~~

Detailed algorithms come later.

---

# 31. Load Shedding

Load shedding intentionally rejects or defers some work to preserve useful work.

Conceptually:

~~~text
Overload
→ Protect Critical Path
→ Drop / Delay Lower-Priority Work
→ Recover
~~~

Rejecting some work can improve overall availability.

---

# 32. Backpressure

Backpressure tells upstream systems that downstream capacity is constrained.

Good backpressure reduces:

- queue explosion
- overload
- wasted retries
- recovery delay

Backpressure must propagate through the chain.

---

# 33. Graceful Degradation

Graceful degradation keeps the most important capability available while reducing non-critical features.

Example:

~~~text
Recommendation Service Fails
→ Checkout Continues Without Recommendations
~~~

This requires knowing what is truly optional.

---

# 34. Critical vs Optional Dependency

Classify dependencies:

~~~text
Critical
Degradable
Optional
Asynchronous
~~~

This classification drives failure behavior.

---

# 35. Isolation / Bulkhead — Preview

Isolation prevents one overloaded or failing area from consuming all shared capacity.

Possible isolation dimensions:

- tenant
- service
- queue
- thread/connection pool
- region
- workload class

Detailed bulkhead patterns come later.

---

# 36. Circuit Breaker — Preview

A circuit breaker can temporarily stop calls to a failing dependency after failure conditions are met.

It is a conditional protection pattern rather than a universal requirement; some architectures already isolate or queue failures effectively elsewhere.

Conceptually:

~~~text
Failures Increase
→ Stop Sending Some Calls
→ Allow Recovery Window
→ Probe
→ Resume Carefully
~~~

Do not treat it as a universal fix.

---

# 37. Redundancy

Redundancy provides alternate capacity or paths.

Examples:

- replicas
- zones
- regions
- backup systems
- duplicate network paths

Redundancy helps only if the alternatives can survive the relevant failure independently enough.

---

# 38. Failover

Failover moves work to an alternate system when the primary cannot serve correctly.

Questions include:

- what detects failure?
- what state is shared?
- how quickly can traffic move?
- is the alternate actually healthy?
- how is recovery validated?

---

# 39. Failover Can Fail

Failover itself can fail because:

- detection is wrong
- state is stale
- secondary lacks capacity
- dependencies are shared
- traffic shift is too aggressive
- credentials/configuration differ

Failover must be tested, not assumed.

---

# 40. Failback — Preview

Failback returns work to the original or preferred system after recovery.

Risks include:

- moving too early
- state divergence
- synchronized traffic movement
- repeating the incident

Recovery is not complete when failover begins.

---

# 41. Active/Active vs Active/Passive — Preview

Active/active:

~~~text
Multiple sites serve traffic
~~~

Active/passive:

~~~text
Primary serves
Secondary waits / prepares
~~~

Each model has state, routing, cost, testing, and consistency trade-offs.

Deep design comes later.

---

# 42. Data Failure

Failure can affect data through:

- loss
- corruption
- duplication
- stale state
- partial write
- inconsistent replication
- accidental deletion

Data recovery is different from service restart.

---

# 43. Backup Is Not Recovery

A backup existing does not prove recovery works.

Recoverability is demonstrated by restoring data, validating that it is usable, and confirming the workload can meet its intended recovery objectives.

Recovery requires:

~~~text
Backup Exists
→ Restore Works
→ Data Is Usable
→ Application Works
→ Business Outcome Validated
~~~

Restore testing matters.

---

# 44. RTO — Preview

Recovery Time Objective asks:

> How long can recovery take?

It is a business/reliability target, not simply a technical metric.

---

# 45. RPO — Preview

Recovery Point Objective asks:

> How much recent data loss is acceptable?

RTO and RPO answer different questions.

Deep disaster-recovery design comes later.

---

# 46. Network Partition — Preview

A network partition occurs when parts of a distributed system cannot communicate reliably with each other.

The system may face difficult choices around:

- availability
- consistency
- leadership
- writes
- stale reads

Formal distributed-systems theory comes later.

---

# 47. Split-Brain — Preview

Split-brain describes situations where multiple sides may believe they are authoritative.

This can create:

- conflicting writes
- duplicate actions
- divergent state

Leadership and quorum mechanisms exist partly to reduce these risks.

---

# 48. Quorum — Preview

A quorum is a minimum agreement threshold used by some distributed systems to make decisions.

At D00, retain:

> Quorum mechanisms are used by some distributed systems to make authority decisions when communication is disrupted.

The exact safety and availability behavior depends on the protocol. The etcd model used in source verification is one majority-based example and must not be generalized to every distributed system.

Detailed mathematics come later.

---

# 49. State Uncertainty

Sometimes the failure is not knowing what happened.

Example:

~~~text
Request Sent
→ Timeout
→ Did Dependency Complete It?
→ Unknown
~~~

This is especially dangerous for side-effecting actions.

Use reconciliation, operation identity, and idempotency where possible.

---

# 50. Duplicate Processing

Failures and retries can create duplicates.

Examples:

- duplicate order
- duplicate message
- duplicate notification
- duplicate resource creation

Exactly-once behavior is difficult; practical systems often design for duplicate detection or idempotent effects.

---

# 51. Change Failure

Many incidents follow change.

Examples:

- bad deployment
- configuration error
- schema incompatibility
- permission change
- certificate change
- dependency upgrade

Change safety is failure prevention.

---

# 52. Configuration Failure

Configuration can fail without code defects.

Examples:

- wrong endpoint
- invalid timeout
- missing environment value
- incorrect permission
- wrong feature flag

Configuration is production behavior.

---

# 53. Security-Control Failure

Security controls can also fail.

Examples:

- overly broad access
- expired credential
- policy blocks legitimate recovery
- secret rotation breaks dependency
- certificate expires

Security and reliability must be designed together.

---

# 54. Human / Process Failure

Failures can involve:

- ambiguous ownership
- wrong approval
- unclear runbook
- fatigue
- incomplete handoff
- unsafe emergency action

Avoid reducing incidents to "human error."

Look at the conditions that made the error likely or impactful.

---

# 55. Observability Failure

A system can fail operationally because the team cannot see what is happening.

Examples:

- missing dependency metrics
- no trace context
- logs missing region/version
- alert fires too late
- health check monitors wrong behavior

Detection is part of resilience.

---

# 56. Alerting Failure

Alerting can fail by:

- missing important incidents
- paging on non-actionable noise
- delayed detection
- poor context
- duplicate alerts

A failed alerting system can extend impact even when the technical failure is unchanged.

---

# 57. Runbook Failure

A runbook can fail when:

- outdated
- too vague
- assumes unavailable access
- skips validation
- ignores partial failure
- has no stop condition

Operational documentation is part of the recovery system.

---

# 58. Control Plane vs Data Plane Failure

A system may separate:

- control plane
- data plane

A control-plane failure may prevent changes while existing traffic still works.

A data-plane failure may affect user traffic while control APIs remain healthy.

The distinction matters for diagnosis and recovery.

---

# 59. Detection

Failure handling begins with noticing meaningful failure.

Detection should answer:

- what outcome is failing?
- who is affected?
- where?
- since when?
- how severe?
- what changed?

---

# 60. Containment

Containment limits propagation.

Possible conceptual actions:

- isolate failing area
- reduce traffic
- stop retries
- shed load
- disable optional feature
- pause rollout
- limit automation

Containment aims to reduce impact before perfect explanation.

---

# 61. Recovery

Recovery moves the system toward an acceptable state.

Recovery may include:

- failover
- rollback
- roll-forward
- restore
- restart
- reconfiguration
- compensation
- traffic shift

The correct recovery action depends on the failure mode.

---

# 62. Recovery Validation

Do not declare recovery because one metric improved.

Validate:

- user outcome
- latency
- errors
- queues
- retries
- dependencies
- data correctness
- regional health
- security state

Recovery is a hypothesis that needs evidence.

---

# 63. Learning

After recovery, ask:

- what failed?
- what assumptions were wrong?
- how did failure propagate?
- what limited blast radius?
- what increased blast radius?
- what detection was missing?
- what should change?

Learning closes the reliability loop.

---

# 64. Pre-Mortem Thinking

A pre-mortem asks:

> Imagine this system failed badly. What likely conditions caused it?

Use it before launch or major change.

This encourages failure discovery before production incidents.

---

# 65. Failure Mode Review

For each critical journey, ask:

~~~text
Dependency Fails
Dependency Slows
Dependency Returns Wrong Data
Dependency Times Out
Dependency Becomes Intermittent
Dependency Becomes Partially Reachable
~~~

Different modes can require different responses.

---

# 66. Failure Testing

Failure testing validates assumptions about degraded behavior and recovery.

Safe principles:

- use controlled non-production or explicitly approved environments
- define hypothesis
- define blast radius
- define stop conditions
- observe impact
- validate recovery
- learn

Do not perform uncontrolled destructive testing.

---

# 67. Fault Injection — Preview

Fault injection deliberately introduces a controlled failure condition for testing.

At D00, focus on the reasoning model:

~~~text
Hypothesis
→ Controlled Fault
→ Observe
→ Stop if Unsafe
→ Recover
→ Validate
→ Learn
~~~

Tooling and real production experiments belong later.

---

# 68. Chaos Engineering — Preview

Chaos engineering is not random destruction.

At foundation level, it means:

- define expected steady behavior
- form a hypothesis
- introduce controlled disturbance
- observe
- protect blast radius
- stop safely
- learn

Production chaos requires mature controls and explicit authorization.

---

# 69. Game Day

A game day is a planned exercise around failure/recovery scenarios.

Possible goals:

- validate communication
- validate runbooks
- test failover assumptions
- test monitoring
- reveal ownership gaps

Game days can be tabletop-only and do not require real destructive actions.

---

# 70. Failure Budget Thinking

Every system accepts some risk.

Questions include:

- which failure modes are tolerable?
- which are unacceptable?
- what blast radius is acceptable?
- how much recovery time is acceptable?
- where is investment justified?

Not every failure deserves the same prevention cost.

---

# 71. Common Beginner Mistakes

## Mistake 1

"Failure means complete outage."

Slow, stale, partial, incorrect, or ambiguous behavior can also be failure.

## Mistake 2

"Add replicas and we are resilient."

Replicas can share the same failure domain.

## Mistake 3

"Retry fixes temporary problems."

Retries can amplify overload or duplicate side effects.

## Mistake 4

"Failover is our recovery plan."

Failover itself can fail and must be validated.

## Mistake 5

"We have backups, so recovery is solved."

Only a successful restore and application validation prove recoverability.

## Mistake 6

"Every incident has one root cause."

Complex incidents can have multiple interacting contributing conditions.

## Mistake 7

"Human error caused it."

Ask why the system allowed one action to have that impact.

## Mistake 8

"Chaos means breaking production."

Safe failure testing is hypothesis-driven, bounded, controlled, and authorized.

---

# 72. Five-Level Explanation

## L1 — Foundation

Failure thinking means asking what can go wrong and how the system behaves when it does.

## L2 — Engineer

Engineers identify failure modes, timeouts, retries, degraded behavior, recovery paths, and dependency risks.

## L3 — Senior Engineer

Senior engineers reason about partial failure, propagation, correlated failure, blast radius, state uncertainty, overload, and recovery validation.

## L4 — SRE / Platform Engineer

SRE uses failure thinking to design graceful degradation, overload protection, failover, recovery exercises, observability, runbooks, and bounded fault testing.

## L5 — Architect

Architects design failure domains, independence, state/recovery strategy, dependency contracts, containment, recovery objectives, and validated resilience across technical and human systems.

---

# 73. Senior Engineer Perspective

A senior engineer asks:

- what are the failure modes?
- is the failure transient, permanent, intermittent, or partial?
- how can it propagate?
- what state becomes uncertain?
- what is the blast radius?
- what retry/timeout behavior exists?
- what containment is available?
- how is recovery validated?

---

# 74. SRE Perspective

An SRE asks:

- which user journey / SLO is affected?
- what is the fastest safe mitigation?
- are retries amplifying failure?
- should load be shed?
- what evidence confirms recovery?
- can the failure be reproduced safely later?
- what runbook or alert gap was exposed?

---

# 75. Architect Perspective

An architect asks:

- which failure domains are truly independent?
- which dependencies are critical vs degradable?
- what state must survive failure?
- what is the acceptable RTO / RPO?
- where can failure be contained?
- where can common-mode failure occur?
- how is failover tested?
- what failure assumptions should be validated before launch?

---

# 76. What You Must Retain

Before moving on, retain:

- fault, error, and failure are related but distinct concepts
- failure mode describes how a system fails
- impact connects failure to user/business/system outcomes
- complete outage is only one failure mode
- slow, stale, incorrect, intermittent, gray, and partial behavior can be failures
- failure domains define correlated scope
- blast radius should be intentionally bounded
- transient and permanent failures need different handling
- dependencies can fail by being slow, incorrect, unavailable, or partially reachable
- correlated/common-mode failure can defeat redundancy
- overload and resource exhaustion are failure modes
- cascading failure follows propagation paths and feedback loops
- timeouts bound waiting
- fail-fast behavior can protect resources and latency budgets
- retries can recover or amplify failure
- load shedding and backpressure protect constrained systems
- graceful degradation depends on knowing what is optional
- isolation limits cross-impact
- circuit breakers are conditional protective mechanisms, not universal fixes
- redundancy needs sufficient independence
- failover itself can fail
- failback has its own risk
- data failure is different from service-process failure
- backup existence does not prove recoverability
- RTO and RPO answer different recovery questions
- network partitions create distributed-state choices
- split-brain and quorum are distributed-systems concerns
- unknown outcomes require reconciliation
- duplicate processing connects failure handling to idempotency
- changes and configuration are major failure sources
- security controls can affect reliability
- human/process conditions influence incidents
- observability and alerting can fail
- runbooks are part of the recovery system
- control plane and data plane can fail differently
- containment can be more urgent than perfect explanation
- recovery must be validated against user/system outcomes
- pre-mortems reveal failure assumptions before incidents
- failure testing should be hypothesis-driven, bounded, controlled, and authorized
- chaos engineering is not random destruction
- game days can safely validate people/process/runbook assumptions
- architecture should price prevention effort against risk and recovery needs

---

# 77. Practical Package — Next Layer

The practical package should include safe, provider-neutral exercises such as:

- classify failure modes for one user journey
- distinguish fault, error, failure, and impact
- map failure domains and blast radius
- classify transient/permanent/intermittent/partial failures
- model a slow-dependency failure chain
- analyze retry amplification and timeout boundaries
- design graceful degradation / backpressure / load shedding conceptually
- review redundancy for common-mode failure
- reason about failover and recovery validation
- distinguish backup existence from restore capability
- perform a pre-mortem / tabletop failure review
- design a safe failure-testing hypothesis with stop conditions

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 78. Assessment Package — Pending

The assessment should test:

- fault / error / failure / impact
- failure modes
- transient / permanent / intermittent / partial failure
- gray / slow / stale / incorrect failure
- dependency failure
- correlated/common-mode failure
- failure domains / blast radius
- overload / resource exhaustion
- cascading failure / propagation
- timeouts / fail-fast
- retries / backoff / amplification
- load shedding / backpressure
- graceful degradation
- isolation / circuit-breaker previews
- redundancy / independence
- failover / failback
- data failure / backup / restore
- RTO / RPO previews
- partition / split-brain / quorum previews
- state uncertainty / duplicates
- change / configuration / security-control failure
- human / process / observability / alerting / runbook failure
- control-plane vs data-plane failure
- containment / recovery / validation / learning
- pre-mortems
- failure testing / fault injection / chaos / game-day previews
- Senior/SRE/Architect reasoning

---

# 79. Visual Package — Pending

The visual package should include:

1. Fault → Error → Failure → Impact → Detection → Recovery
2. Failure Modes: Down / Slow / Stale / Wrong / Partial / Intermittent
3. Dependency Failure → Retry → Saturation → Cascading Failure
4. Failure Domain → Redundancy → Common-Mode Failure → Blast Radius
5. Detect → Contain → Recover → Validate → Learn
6. Hypothesis → Controlled Failure Test → Observe → Stop → Recover → Learn

---

# 80. What Comes Next

After D00-T018 is completed, continue to:

## 00.19 — Troubleshooting Mental Model

That topic will deepen evidence-first diagnosis, scoping, timelines, hypothesis ranking, safe tests, mitigation, validation, RCA, and prevention.

---

# 81. Sources & Evidence

Planned authoritative source families:

- Google SRE guidance on cascading failure, overload, retries, recovery, and reliability
- AWS / Azure / Google Cloud resilience guidance
- Kubernetes disruption, failure-domain, and control-plane behavior documentation
- CNCF / resilience engineering references
- chaos-engineering principles at a conceptual level
- distributed-systems references for partitions, quorum, failover, and state uncertainty
- disaster-recovery references for backup/restore, RTO, and RPO

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: pending
- assessment package: pending
- visual package: pending

Detailed verification record:

- [D00-T018 Source Verification](../../../../docs/sources/D00/D00-T018-source-verification.md)

Verified nuances:

- failure mode should describe how a workload degrades and what impact becomes visible
- fault/error/failure terminology varies across disciplines, so the topic preserves a conceptual chain instead of claiming one universal formal wording
- complete outage is only one failure form; slow, stale, incorrect, intermittent, partial, or observer-dependent behavior can also matter
- retries are part of failure propagation and can amplify overload
- graceful degradation and load shedding can preserve critical functionality under stress
- circuit breakers are conditional protection mechanisms, not universal fixes
- redundancy does not prove independence from common-mode failure
- failover is itself an operation with assumptions, capacity requirements, and failure modes
- backup existence does not prove recoverability; restore and workload validation are required
- RTO and RPO are distinct business-driven recovery objectives
- network-partition and quorum behavior is protocol-specific and remains preview-level
- containment can be prioritized before perfect explanation during active user impact
- recovery must be validated end-to-end
- resilience testing should be hypothesis-driven, bounded, observable, recoverable, and authorized
- chaos engineering is controlled experimentation, not random destruction
