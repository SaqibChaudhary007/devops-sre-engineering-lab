# D00-T018 Source Verification — Failure Thinking

## Verification Goal

Verify the core claims in **00.18 — Failure Thinking** against authoritative SRE, cloud reliability, distributed-systems, disaster-recovery, and chaos-engineering guidance.

Primary source families used:

- Google SRE guidance on cascading failure, overload, retries, and graceful degradation
- Microsoft Azure Well-Architected failure-mode analysis, self-preservation, circuit-breaker, transient-fault, and reliability-testing guidance
- AWS Well-Architected fault isolation, backup/recovery, disaster recovery, chaos engineering, and game-day guidance
- etcd distributed-systems failure-mode documentation for network partitions and majority/quorum behavior
- Principles of Chaos Engineering for hypothesis-driven, measurable, blast-radius-limited experiments

## Verification Status

**Result:** Core D00-T018 claims are supported, with important nuances around failure-mode analysis, fault isolation, overload, retry amplification, graceful degradation, recovery objectives, backup/restore validation, failover assumptions, partitions/quorum, and safe resilience testing.

**Evidence level:** E2 — supported by first-party engineering documentation, established SRE guidance, cloud-provider reliability frameworks, and authoritative distributed-systems documentation.

This topic remains at the D00 mental-model level. Formal FMEA/FTA methods, distributed-consensus proofs, quorum mathematics, production chaos tooling, advanced DR topology design, fault-injection platforms, and platform-specific recovery engineering belong to later domains.

---

# Primary / Authoritative Sources

## 1. Microsoft Azure Well-Architected — Failure Mode Analysis

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/failure-mode-analysis

Supports:

- workloads should be decomposed into flows and dependencies
- failure modes should be identified explicitly
- blast radius should be considered for each failure
- mitigation and detection should be designed before incidents
- resilient systems assume failures will occur

### Verified nuance

Failure thinking should begin with:

~~~text
Flow / Dependency
→ Failure Mode
→ Blast Radius
→ Detection
→ Mitigation
→ Recovery
~~~

"Service failed" is too vague to be useful without describing **how** it failed and what outcome was affected.

---

## 2. Google SRE — Addressing Cascading Failures

- https://sre.google/sre-book/addressing-cascading-failures/

Supports:

- cascading failures can grow through positive feedback
- overload is a major source of cascading failure
- retries can amplify load and destabilize recovery
- resource exhaustion can spread across CPU, memory, threads, connections, and remaining replicas
- retries should be bounded and should distinguish retriable from non-retriable conditions

### Verified nuance

The D00 propagation model is supported:

~~~text
Dependency Slows
→ Timeouts
→ Retries
→ More Load
→ Resource Exhaustion
→ Wider Failure
~~~

Retries are a reliability tool only when their side effects, limits, and dependency state are understood.

---

## 3. Google SRE — Handling Overload

- https://sre.google/sre-book/handling-overload/
- https://sre.google/sre-book/service-best-practices/

Supports:

- overload must be handled intentionally
- graceful degradation can preserve useful service
- some requests may need to be rejected under severe overload
- retry behavior must consider whether the system is globally overloaded
- load shedding and bounded queuing can improve useful throughput and recovery

### Verified nuance

Rejecting or deferring some work can improve reliability.

At D00:

~~~text
Overload
→ Protect Critical Work
→ Degrade / Shed Lower-Priority Work
→ Reduce Pressure
→ Recover
~~~

"Serve everything at any cost" is not always the reliable behavior.

---

## 4. Azure Well-Architected — Graceful Degradation and Self-Preservation

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/self-preservation
- https://learn.microsoft.com/en-us/azure/well-architected/mission-critical/mission-critical-application-design

Supports:

- workloads should have explicit degraded modes
- failed dependencies should not automatically take down all user functionality
- retries, circuit breakers, and health models must differentiate transient from more persistent faults
- degraded behavior should preserve business-critical functionality where possible

### Verified nuance

Graceful degradation requires knowing which capabilities are:

~~~text
Critical
Degradable
Optional
Asynchronous
~~~

It is an architectural decision, not an automatic fallback.

---

## 5. Azure Architecture Center — Circuit Breaker

- https://learn.microsoft.com/en-us/azure/architecture/patterns/circuit-breaker

Supports:

- circuit breakers can prevent repeated calls to a malfunctioning dependency
- circuit breakers can reduce pressure on recovering dependencies
- circuit breakers may support graceful degradation
- the pattern is not appropriate in every architecture

### Verified nuance

Do not teach:

~~~text
Dependency Problems
→ Always Add Circuit Breaker
~~~

A circuit breaker is one conditional protection mechanism among several.

---

## 6. Azure Well-Architected — Transient Fault Handling

- https://learn.microsoft.com/en-us/azure/well-architected/reliability/handle-transient-faults

Supports:

- retries should be finite
- retries should distinguish transient from non-transient faults
- backoff should increase retry spacing
- randomization/jitter can reduce synchronized retries
- retry strategies should be tested under realistic load

### Verified nuance

Transient failure does not mean:

~~~text
Retry Immediately Forever
~~~

A stronger model is:

~~~text
Classify
→ Check Retry Safety
→ Bound Attempts
→ Backoff / Jitter
→ Respect Time Budget
→ Stop / Escalate
~~~

---

## 7. AWS Well-Architected — Fault Isolation

- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel-10.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/use-fault-isolation-to-protect-your-workload.html

Supports:

- fault isolation limits failure impact to a defined boundary
- multiple fault-isolated boundaries can improve resilience
- bulkhead-style isolation can contain impact

### Verified nuance

Redundancy and fault isolation are related but not identical.

Two replicas that share the same failing dependency may still occupy one effective failure domain.

---

## 8. AWS Well-Architected — Backup and Restore Validation

- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel-09.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_backing_up_data_periodic_recovery_testing_data.html

Supports:

- backup existence alone does not prove recoverability
- backups should be restored periodically
- restored data should be checked for usability, integrity, accessibility, and recovery-objective compliance
- restore procedures should be repeatable and tested

### Verified nuance

The D00 model is correct:

~~~text
Backup Exists
→ Restore Works
→ Data Is Usable
→ Application Works
→ Business Outcome Validated
~~~

"Backup successful" is not the same as "recovery proven."

---

## 9. AWS Well-Architected — RTO / RPO and Disaster Recovery

- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel-13.html
- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_planning_for_recovery_disaster_recovery.html

Supports:

- RTO is a recovery-time target
- RPO is a data-loss / recovery-point target
- recovery strategies should be selected against business objectives
- backup/restore, pilot light, warm standby, and active/active strategies have different cost/recovery trade-offs
- recovery strategies should be tested rather than assumed

### Verified nuance

RTO and RPO answer different questions:

~~~text
RTO
→ How long can recovery take?

RPO
→ How much recent data loss is acceptable?
~~~

They are business-driven objectives, not automatically chosen infrastructure metrics.

---

## 10. etcd — Failure Modes / Network Partition

- https://etcd.io/docs/v3.5/op-guide/failures/

Supports:

- a network partition can split a distributed cluster into majority and minority sides
- majority availability governs continued cluster operation
- minority members cannot continue authoritative operation
- majority-based coordination reduces split-brain behavior

### Verified nuance

At D00:

~~~text
Partition
→ Some Members Cannot Communicate
→ Authority / Availability Decision
→ Majority / Quorum Matters
~~~

Do not generalize one consensus system's exact behavior to every distributed system.

---

## 11. AWS Well-Architected — Reliability Testing and Game Days

- https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/test-reliability.html
- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_testing_resiliency_game_days_resiliency.html

Supports:

- resilience assumptions should be tested
- game days exercise systems, processes, runbooks, and teams
- experiments should be planned and monitored
- if harmful behavior is observed, the experiment should be stopped/rolled back and lessons captured
- testing should include realistic operational conditions

### Verified nuance

Failure testing is not random breakage.

A safe model is:

~~~text
Hypothesis
→ Controlled Scenario
→ Observe
→ Stop if Unsafe
→ Recover
→ Validate
→ Learn
~~~

---

## 12. Principles of Chaos Engineering

- https://principlesofchaos.org/

Supports:

- chaos engineering is an experimental discipline
- experiments should begin with measurable steady-state behavior
- experiments should form a hypothesis
- real-world disruptive conditions are introduced deliberately
- blast radius should be minimized and contained
- the goal is to uncover systemic weaknesses and build confidence

### Verified nuance

Do not teach:

~~~text
Chaos Engineering
→ Random Destruction
~~~

A stronger foundation model is:

~~~text
Steady-State Measure
→ Hypothesis
→ Controlled Disturbance
→ Observe Difference
→ Minimize Blast Radius
→ Learn
~~~

For this curriculum, practical work remains safe and local/provider-neutral; production experimentation belongs to later maturity levels and explicit authorization.

---

# Verified Claim Map

| Topic claim | Verification | Primary source family |
|---|---|---|
| Failure modes should be identified explicitly | Verified | Azure FMA |
| Blast radius should be analyzed | Verified | Azure / AWS |
| Failures can propagate through feedback | Verified | Google SRE |
| Overload can create cascading failure | Verified | Google SRE |
| Retries can amplify overload | Verified | Google SRE / Azure |
| Retries should be bounded | Verified | Google SRE / Azure |
| Graceful degradation can preserve critical functionality | Verified | Google SRE / Azure |
| Load shedding can protect useful work | Verified | Google SRE |
| Circuit breaker is a conditional protection pattern | Verified | Azure |
| Fault isolation limits scope of impact | Verified | AWS |
| Redundancy alone does not prove failure independence | Verified at mental-model level | AWS fault isolation |
| Backup existence does not prove recovery | Verified | AWS |
| Restore testing validates recoverability | Verified | AWS |
| RTO and RPO are distinct recovery objectives | Verified | AWS |
| DR strategy should be selected against recovery objectives | Verified | AWS |
| Network partitions require authority/availability decisions | Verified | etcd |
| Majority/quorum behavior can prevent incompatible authoritative sides | Verified in etcd context | etcd |
| Resilience assumptions should be tested | Verified | AWS |
| Game days test systems/processes/team response | Verified | AWS |
| Chaos engineering is hypothesis-driven experimentation | Verified | Principles of Chaos |
| Chaos experiments should minimize blast radius | Verified | Principles of Chaos |

---

# Verified Nuances / Corrections

## 1. Fault / Error / Failure Terminology Can Vary

Different reliability and safety traditions use these terms with slightly different formal definitions.

At D00, retain the conceptual relationship:

~~~text
Fault / Stressor
→ Incorrect Internal State / Degradation
→ Externally Visible Failure
~~~

Do not overfit to one vocabulary.

## 2. Failure Is Not Only "Down"

A workload can fail by being:

- unavailable
- too slow
- stale
- incorrect
- partial
- intermittent
- ambiguous

The exact label "gray failure" is useful as a mental model, but the source set more directly verifies partial/degraded and observer-dependent failure behavior than one universal formal definition of that term.

## 3. Failure Domain Is About Correlated Scope

A failure domain is useful only relative to a failure being considered.

Two zones may be independent for one infrastructure failure but still share:

- control plane
- identity
- deployment
- dependency
- configuration

for another.

## 4. Retry Is Part of Failure Propagation

Retries are not isolated client behavior.

At multiple layers they can multiply work dramatically and slow recovery.

## 5. Fail-Fast and Load Shedding Are Protective Behaviors

Rejecting work can sometimes preserve the ability to serve critical work.

Availability should be evaluated by useful user outcome, not by accepting every request.

## 6. Graceful Degradation Must Be Designed

The system must know which functionality can be reduced or disabled safely.

Degradation without product/business understanding can produce incorrect outcomes.

## 7. Circuit Breakers Are Not Universal

Some architectures may already have effective failure isolation, queue-based handling, platform-level recovery, or other mechanisms.

Use the pattern only where it solves a real failure mode.

## 8. Redundancy Is Not Independence

Replicas can still fail together through shared:

- database
- region
- network
- credentials
- deployment
- operator action

The relevant failure domains must be examined explicitly.

## 9. Failover Is an Operation That Can Fail

A secondary may be:

- under-capacity
- stale
- misconfigured
- dependent on the same failing service
- unreachable through the same control path

Failover needs detection, capacity, state, routing, and validation.

## 10. Backup Is Evidence of Protection, Not Proof of Recovery

Recovery is proven only by restoring and validating usable data and service behavior against recovery objectives.

## 11. RTO and RPO Are Business Objectives

Do not infer them from existing infrastructure capability.

Business tolerance should drive the target, then architecture should be selected to meet it.

## 12. Partition / Split-Brain / Quorum Must Stay Preview-Level

The exact safety/liveness behavior depends on the distributed protocol.

The etcd source verifies one majority-based model; do not generalize its exact mechanics to every database or cluster.

## 13. Containment Can Precede Perfect Explanation

During active impact, reducing blast radius or stabilizing the system can be more urgent than completing root-cause analysis.

Evidence should still guide the mitigation.

## 14. Recovery Must Be Validated End-to-End

One green health check or improved CPU graph does not prove recovery.

Validate the user journey, queues, retries, dependencies, data correctness, and security/recovery state as relevant.

## 15. Failure Testing Is a Controlled Engineering Activity

Safe failure testing requires:

- hypothesis
- defined scope
- expected behavior
- observability
- stop conditions
- recovery plan
- authorization
- post-test learning

## 16. Chaos Engineering Is Not Random Production Destruction

The Principles of Chaos Engineering explicitly frame chaos as controlled experimentation around steady-state behavior and systemic weaknesses.

Production experiments require mature safeguards and authorization; D00 practical exercises should remain safe and bounded.

---

# Evidence Decision

The following D00-T018 areas are now eligible for **DOC-VERIFIED** status:

- fault/error/failure conceptual relationship
- failure modes
- impact
- failure domains / blast radius
- transient vs persistent/non-transient failure at foundation level
- intermittent / partial / degraded failure at foundation level
- slow/stale/incorrect behavior as failure possibilities
- dependency failure
- correlated / common-mode failure
- overload / resource exhaustion
- cascading failure / propagation / amplification
- timeout boundaries
- fail-fast reasoning
- retry amplification
- backoff / jitter connection
- load shedding
- backpressure
- graceful degradation
- critical vs optional dependency classification at mental-model level
- isolation / bulkhead preview
- circuit-breaker preview
- redundancy / independence
- failover / failback reasoning at foundation level
- data failure
- backup vs restore
- RTO / RPO preview
- partition / quorum preview
- state uncertainty / duplicate-processing connection
- change/configuration/security-control failure at mental-model level
- human/process/observability/alerting/runbook failure at mental-model level
- containment / recovery / validation / learning
- pre-mortem reasoning
- resilience/failure testing
- game-day preview
- chaos-engineering preview

The following remain intentionally preview-level pending later domains:

- formal FMEA scoring
- fault-tree analysis
- quantitative reliability block diagrams
- CAP theorem depth
- consensus / quorum mathematics
- split-brain prevention algorithms
- distributed lock/lease internals
- production fault-injection tooling
- chaos automation platforms
- advanced multi-region failover
- database-specific recovery algorithms
- storage consistency models
- detailed DR architecture selection
- forensic incident handling
- formal safety engineering

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured, safe exercises:

- classify failure modes for one user journey
- distinguish fault, internal error/degradation, externally visible failure, and impact
- map failure domains and blast radius
- classify transient / permanent / intermittent / partial conditions
- model a slow-dependency failure chain
- analyze retry amplification and timeout boundaries
- design graceful degradation / backpressure / load shedding conceptually
- review redundancy for common-mode failure
- reason about failover and recovery validation
- distinguish backup existence from restore capability
- perform a pre-mortem / tabletop failure review
- design a safe failure-testing hypothesis with explicit stop conditions

These become the D00-T018 practical package.
