---
id: D00-T017
domain: D00
title: Systems Thinking
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
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Follow the Request
  - Five Levels
  - Production Room
  - Think Like SRE
  - Architecture With Saqib
---

# 00.17 — Systems Thinking

## Start Here

You now understand applications, infrastructure, distributed systems, reliability, SRE, observability, security, and automation.

The next question is:

> How do we reason about the behavior of the whole system when each component can look healthy, every team can optimize locally, and the overall outcome can still be poor?

That is the problem space of **systems thinking**.

Systems thinking is not:

- drawing architecture boxes only
- blaming one component for every symptom
- optimizing each team independently
- assuming cause and effect are immediate
- treating every dependency as equal
- believing more capacity always solves the problem
- assuming local improvements always improve the whole
- analyzing incidents as isolated events
- ignoring human, process, policy, and organizational feedback loops

The core mental model is:

~~~text
System Boundary
→ Components
→ Relationships
→ Flows
→ Constraints
→ Feedback
→ Delays
→ Behavior Over Time
→ Intervention
→ New Behavior
~~~

A second useful model is:

~~~text
Local Action
→ System Interaction
→ Second-Order Effects
→ Global Outcome
~~~

Systems thinking helps engineers move from component-level reasoning to end-to-end behavior, feedback loops, bottlenecks, coupling, delays, emergent behavior, and trade-offs.

This D00 topic stays at the foundational mental-model level. Formal systems dynamics, queueing theory, graph theory, advanced control theory, distributed-systems proofs, organization design, and quantitative modeling come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- system
- system boundary
- environment
- component
- relationship
- dependency
- flow
- input
- output
- state
- constraint
- bottleneck
- throughput
- latency
- queue
- capacity
- saturation
- feedback loop
- reinforcing loop
- balancing loop
- delay
- lag
- accumulation / stock
- rate / flow
- coupling
- tight coupling
- loose coupling
- hidden coupling
- nonlinearity
- threshold effects
- local optimization
- global optimization
- emergent behavior
- second-order effects
- side effects
- trade-offs
- leverage points
- failure propagation
- blast radius
- cascading failure
- redundancy
- dependency chains
- critical path
- weakest link thinking
- resource contention
- backpressure
- retries as feedback
- autoscaling as feedback
- alerting as feedback
- automation as feedback
- human/operator feedback
- organizational incentives
- observability gaps
- feedback quality
- stability
- oscillation
- over-correction
- delayed correction
- system archetype previews
- SLOs as system outcomes
- architecture decisions as interventions
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

You should already understand dependencies, queues, retries, saturation, blast radius, reconciliation, SLOs, incidents, and observability.

---

# 3. What Is a System?

A system is a set of interacting elements that together produce behavior or outcomes.

Examples:

- checkout platform
- Kubernetes cluster
- CI/CD delivery path
- incident-response process
- organization
- service + database + queue + external dependencies

The important idea is not the number of components.

It is the **interaction** between them.

---

# 4. System Boundary

A system boundary defines what you include in your analysis.

Example:

~~~text
Narrow Boundary:
Application Service Only

Wider Boundary:
User
→ DNS
→ CDN / LB
→ Application
→ Database
→ Queue
→ External Payment
→ Operations
~~~

The chosen boundary changes what causes and solutions you can see.

There is not always one universally correct boundary; the boundary should be appropriate to the question and outcome being studied.

---

# 5. Environment

A system exists inside an environment.

The environment may include:

- users
- traffic patterns
- cloud-provider behavior
- external APIs
- network conditions
- team processes
- business policy
- cost constraints

A system can behave differently when the environment changes.

---

# 6. Component Thinking vs System Thinking

Component thinking asks:

> Is this service healthy?

System thinking asks:

> Is the complete user outcome healthy, and how are components interacting to produce that result?

A component can be healthy while the system outcome is poor.

---

# 7. Relationships Matter

A component's behavior often depends on:

- upstream traffic
- downstream capacity
- queue state
- retry behavior
- timeout settings
- shared resources
- policy
- operator actions

Relationships can matter more than component internals.

---

# 8. Inputs and Outputs

Every useful system model should identify:

~~~text
Inputs
→ Transformation
→ Outputs
~~~

For a checkout service:

~~~text
Traffic + Inventory + Payment Availability
→ Checkout Processing
→ Successful Orders / Failures / Delays
~~~

Inputs can vary over time.

---

# 9. Flows

Flows move through a system.

Examples:

- requests
- messages
- data
- money
- configuration
- deployment changes
- incidents
- decisions

Flow rate influences queues, capacity, and delay.

---

# 10. State

State accumulates information about the system.

Examples:

- queue backlog
- current deployment version
- database connections
- open incidents
- pending approvals
- retry backlog

State makes behavior depend on history, not only current input.

---

# 11. Constraints

A constraint limits system behavior.

Examples:

- database connection pool
- CPU capacity
- API quota
- worker count
- approval capacity
- budget
- team availability

Constraints often determine throughput.

---

# 12. Bottleneck

A bottleneck is the constraint that limits overall system performance.

The active bottleneck can move after an intervention, so the whole flow should be measured again after meaningful changes.

If every other component becomes faster but the bottleneck does not change, total throughput may barely improve.

---

# 13. Bottleneck Migration

Fixing one bottleneck can expose another.

Example:

~~~text
Increase API Capacity
→ More Requests Reach Database
→ Database Becomes New Bottleneck
~~~

Optimization changes the system.

---

# 14. Local Optimization

A team may optimize its own component:

~~~text
Service A Throughput ↑
~~~

but create more load downstream.

Local improvement does not guarantee global improvement.

---

# 15. Global Optimization

Global optimization asks:

> What change improves the end-to-end outcome?

Examples:

- reduce unnecessary retries
- protect a constrained dependency
- smooth arrival rate
- reduce queue age
- improve cache behavior
- change workflow

The best global solution may reduce activity in one component.

---

# 16. Throughput

Throughput is the amount of useful work completed in a period.

Examples:

- orders/minute
- requests/second
- jobs/hour

High traffic does not necessarily mean high useful throughput.

---

# 17. Latency

Latency is the time required for work to complete.

End-to-end latency may include:

- processing
- queue wait
- network delay
- retries
- dependency delay
- lock wait

Optimizing only CPU time can miss most latency.

---

# 18. Queue

A queue stores work waiting to be processed.

Queues create:

- buffering
- decoupling
- delay
- hidden accumulation

A queue can absorb bursts temporarily but also hide growing instability.

---

# 19. Accumulation / Stock

A stock is something that accumulates over time.

Examples:

- queue backlog
- open tickets
- unresolved vulnerabilities
- technical debt
- retry backlog

Stocks change according to inflow and outflow.

---

# 20. Rate / Flow

A flow changes a stock.

Example:

~~~text
Incoming Jobs
→ Queue
→ Completed Jobs
~~~

If:

~~~text
Arrival Rate > Processing Rate
~~~

the queue grows.

---

# 21. Capacity

Capacity is how much work the system can safely handle.

Capacity is not just infrastructure size.

It may include:

- connection limits
- external quotas
- human response capacity
- database write rate
- queue-consumer capacity

---

# 22. Saturation

Saturation occurs when a resource approaches its useful limit.

Near saturation, systems often become:

- slower
- more variable
- more failure-prone
- more sensitive to bursts

---

# 23. Feedback Loop

A feedback loop occurs when system output influences future system behavior.

Example:

~~~text
Latency ↑
→ Retries ↑
→ Load ↑
→ Latency ↑
~~~

This loop can amplify failure.

---

# 24. Reinforcing Loop

A reinforcing loop amplifies change.

Example:

~~~text
More Errors
→ More Retries
→ More Load
→ More Errors
~~~

Reinforcing loops can drive runaway behavior.

---

# 25. Balancing Loop

A balancing loop pushes the system toward a target or stable condition.

Example:

~~~text
CPU ↑
→ Autoscaling Adds Capacity
→ CPU ↓
~~~

Balancing loops can stabilize systems if delays and thresholds are well designed.

---

# 26. Delay

A delay exists when cause and visible effect are separated in time.

Examples:

- scaling takes minutes
- queue backlog takes time to drain
- cache warm-up takes time
- configuration propagation is delayed
- humans take time to respond

Delays make diagnosis harder.

---

# 27. Delayed Feedback

A system may continue acting because the effect of the previous action is not visible yet.

Example:

~~~text
Scale Up
→ Effect Not Yet Visible
→ Scale Up Again
→ Too Much Capacity Later
~~~

Delayed feedback can cause over-correction.

---

# 28. Oscillation

Oscillation happens when a system repeatedly overshoots and undershoots.

Example:

~~~text
Load High
→ Scale Up
→ Load Low
→ Scale Down
→ Load High
→ Scale Up
~~~

Poor thresholds and delays can create instability.

---

# 29. Stability

A stable system returns toward acceptable behavior after disturbance.

Stability depends on:

- feedback
- delay
- gain / strength of action
- capacity
- guardrails

At D00, focus on the concept rather than control-theory math.

---

# 30. Nonlinearity

Systems are often nonlinear.

A small change can have:

- almost no effect
- gradual effect
- sudden large effect after threshold

Example:

~~~text
Traffic ↑ slightly
→ Connection Pool Saturates
→ Latency ↑ sharply
~~~

---

# 31. Threshold Effect

A threshold is a point where behavior changes significantly.

Examples:

- queue capacity reached
- memory pressure triggers eviction
- rate limit activates
- autoscaler threshold reached

Thresholds create sudden behavior shifts.

---

# 32. Coupling

Coupling describes how strongly one part depends on another.

Tight coupling means one component's behavior strongly affects another.

Loose coupling reduces direct dependency but does not eliminate all interaction.

---

# 33. Hidden Coupling

Hidden coupling exists when systems appear independent but share:

- database
- network
- IAM quota
- DNS
- external API
- deployment pipeline
- human operator

Shared hidden resources create unexpected correlated failure.

---

# 34. Dependency Chain

A user journey may depend on many systems:

~~~text
User
→ DNS
→ Load Balancer
→ API
→ Auth
→ Database
→ Payment
→ Queue
~~~

End-to-end reliability depends on the chain, not only one service.

---

# 35. Critical Path

The critical path is the sequence of work that determines end-to-end completion time.

Improving a non-critical step may not improve user latency.

---

# 36. Weakest-Link Thinking

A system can be limited by its weakest dependency.

But "weakest link" is not always static.

The weakest point can change by:

- traffic
- region
- time
- workload
- failure mode

---

# 37. Resource Contention

Multiple workloads can compete for the same resource.

Examples:

- CPU
- memory
- disk I/O
- database connections
- queue workers
- network bandwidth
- human attention

Contention creates cross-impact.

---

# 38. Backpressure

Backpressure slows or limits incoming work when downstream capacity is constrained.

Conceptually:

~~~text
Downstream Saturated
→ Reduce / Delay Upstream Work
~~~

Without backpressure, queues and retries can grow uncontrollably.

---

# 39. Retry as Feedback

Retries form a feedback loop.

Healthy case:

~~~text
Transient Failure
→ Small Bounded Retry
→ Recovery
~~~

Unhealthy case:

~~~text
Dependency Slow
→ Retries Increase
→ Load Increases
→ Dependency Slower
~~~

---

# 40. Autoscaling as Feedback

Autoscaling observes load and changes capacity.

Conceptually:

~~~text
Observe
→ Compare to Target
→ Add / Remove Capacity
→ Observe Again
~~~

It can fail when:

- signal is poor
- delay is long
- scale action is too aggressive
- bottleneck is somewhere else

---

# 41. Alerting as Feedback

Alerts create a human feedback loop.

~~~text
System Signal
→ Alert
→ Human Decision
→ Action
→ System Change
~~~

Bad alerts create poor feedback.

---

# 42. Automation as Feedback

Automation can close the loop automatically.

~~~text
Detect
→ Decide
→ Act
→ Validate
~~~

If detection is wrong, automation can make the system worse faster.

---

# 43. Human Feedback Loop

Humans are part of production systems.

Examples:

- on-call response
- approval delays
- manual scaling
- rollback decisions
- incident coordination

Human capacity and incentives affect system behavior.

---

# 44. Organizational Incentives

Teams optimize what they are measured on.

Example:

~~~text
Team A Goal: Max Throughput
Team B Goal: Protect Database
~~~

Conflicting goals can create system-level friction.

---

# 45. Goodhart-Style Warning

When a metric becomes a target, behavior may optimize the metric rather than the real outcome.

At D00:

> Measure what matters, but do not assume one metric fully represents the system goal.

---

# 46. Emergent Behavior

Emergent behavior is behavior that appears from interaction among parts rather than from one component alone.

Examples:

- retry storms
- cascading failure
- queue oscillation
- thundering-herd effects
- alert storms

---

# 47. Cascading Failure

A cascading failure spreads from one component to others.

Example:

~~~text
Database Slow
→ API Latency
→ Retries
→ Connection Growth
→ Queue Growth
→ More Saturation
~~~

Understanding propagation paths is key.

---

# 48. Blast Radius

Blast radius asks:

> How much of the system can one failure affect?

Blast radius can be reduced by:

- isolation
- segmentation
- bounded retries
- rate limits
- circuit-breaking patterns
- independent failure domains

Detailed patterns come later.

---

# 49. Redundancy and Common Failure

Redundancy helps only when redundant paths are sufficiently independent for the failure being considered.

Example:

~~~text
Two Services
but
Same Database / Same Region / Same Credential
~~~

The system may still have one effective failure domain.

---

# 50. Second-Order Effects

A second-order effect is the consequence of a consequence.

Example:

~~~text
Add Cache
→ Database Load ↓
→ Traffic Capacity ↑
→ Downstream Payment Load ↑
~~~

Good design asks what happens after the first improvement succeeds.

---

# 51. Side Effects

An intervention can create unintended effects.

Example:

~~~text
Increase Retry Count
→ More Successful Requests
but also
→ More Dependency Load
~~~

Every architecture decision changes multiple relationships.

---

# 52. Trade-Off

Systems thinking expects trade-offs.

Examples:

- latency vs cost
- availability vs consistency
- security vs convenience
- automation vs human control
- redundancy vs complexity

There is rarely a free improvement.

---

# 53. Leverage Point

A leverage point is a place where a relatively small change can produce a large system improvement.

Examples:

- reduce duplicate work
- fix one shared bottleneck
- change timeout policy
- improve feedback signal
- change queue admission policy

The highest leverage change is not always the largest change.

---

# 54. Symptoms vs Structure

Symptoms are visible outcomes.

Structure is the system arrangement producing them.

Example:

~~~text
Symptom:
High Latency

Possible Structure:
Unbounded Retries
+ Shared Dependency
+ No Backpressure
+ Delayed Scaling
~~~

Fixing symptoms alone can leave the structure unchanged.

---

# 55. Event vs Pattern vs Structure

A useful ladder:

~~~text
Event
→ What happened?

Pattern
→ What keeps happening?

Structure
→ What relationships create the pattern?

Mental Model / Policy
→ Why was the structure designed this way?
~~~

Systems thinking moves downward through these layers.

---

# 56. One Incident Is Not the Whole Story

A single outage may be the visible event.

Ask:

- has this happened before?
- under what conditions?
- what recurring pattern exists?
- what structural relationship enables it?

Repeated incidents often indicate system structure.

---

# 57. Observability and Systems Thinking

Observability provides evidence about relationships and flows.

Useful system-level evidence includes:

- dependency latency
- queue age
- retry rate
- saturation
- change markers
- throughput
- user outcome

Component dashboards alone can hide global behavior.

---

# 58. SLOs as System Outcomes

An SLO should represent a meaningful service outcome.

Systems thinking asks:

> What system relationships influence this SLO?

Example:

~~~text
Checkout SLO
depends on
API + Auth + Database + Payment + Queue + Capacity + Change Safety
~~~

---

# 59. Architecture as Intervention

Architecture decisions are interventions in system behavior.

Examples:

- add queue
- introduce cache
- split service
- add retry
- isolate tenant
- add automation

Each intervention changes flows, delays, feedback, and failure modes.

---

# 60. More Capacity Is Not Always the Answer

Adding capacity helps only when capacity is the limiting constraint.

If the issue is:

- lock contention
- external quota
- retry storm
- poor query
- queue age
- shared dependency

more CPU may not help.

---

# 61. Faster Is Not Always Better

Speeding one component can overload the next.

Example:

~~~text
Producer Faster
→ Queue Fills Faster
→ Consumer Saturates
→ End-to-End Latency Worsens
~~~

Optimize the flow, not only the component.

---

# 62. More Redundancy Is Not Always Safer

More replicas can increase:

- coordination cost
- shared-resource pressure
- control-plane complexity
- failure correlation

Redundancy must be architected, not counted.

---

# 63. Common Beginner Mistakes

## Mistake 1

"Every problem has one root cause."

Complex systems can have multiple contributing conditions.

## Mistake 2

"If every service is healthy, the system is healthy."

Interactions can still produce poor outcomes.

## Mistake 3

"Optimize every component."

Local optimization can harm the global outcome.

## Mistake 4

"More capacity fixes performance."

Only if capacity is the limiting constraint.

## Mistake 5

"More retries improve reliability."

Retries can create reinforcing failure loops.

## Mistake 6

"Redundancy always removes failure."

Shared dependencies can create common-mode failure.

## Mistake 7

"Cause and effect are immediate."

Delays can hide the relationship.

## Mistake 8

"Humans are outside the system."

Operators, incentives, and approvals influence production behavior.

---

# 64. Five-Level Explanation

## L1 — Foundation

Systems thinking means understanding how parts interact to create the behavior of the whole.

## L2 — Engineer

Systems thinking connects dependencies, flows, queues, capacity, bottlenecks, feedback, and delays.

## L3 — Senior Engineer

Senior engineers reason about local vs global optimization, coupling, cascading failure, backpressure, second-order effects, and observability across the full user journey.

## L4 — SRE / Platform Engineer

SRE applies systems thinking to SLOs, retries, autoscaling, alerts, automation, capacity, incident patterns, and operational feedback loops.

## L5 — Architect

Architects design boundaries, dependencies, feedback, incentives, failure domains, and interventions to create stable, scalable, evolvable systems.

---

# 65. Senior Engineer Perspective

A senior engineer asks:

- what is the system boundary?
- what is flowing?
- what state is accumulating?
- where is the bottleneck?
- what is the critical path?
- what feedback loop exists?
- what delays exist?
- what second-order effect could occur?
- what is the global outcome?

---

# 66. SRE Perspective

An SRE asks:

- which SLO is affected?
- what reinforcing loop is amplifying failure?
- is the queue growing?
- are retries worsening saturation?
- is autoscaling reacting too slowly?
- are alerts creating useful feedback?
- what intervention stabilizes the system?

---

# 67. Architect Perspective

An architect asks:

- where are system boundaries?
- where is coupling too tight?
- where are common failure domains?
- what bottleneck will appear next?
- what feedback loops are stable or unstable?
- what intervention has the highest leverage?
- what new behavior might appear after the change?

---

# 68. What You Must Retain

Before moving on, retain:

- a system is defined by interactions, not just components
- boundaries affect what causes and solutions you can see
- inputs, outputs, state, and constraints shape behavior
- bottlenecks limit global throughput
- fixing one bottleneck can expose another
- local optimization can harm global outcomes
- queues create both buffering and delay
- stocks accumulate when inflow exceeds outflow
- saturation increases latency and instability
- feedback loops can reinforce or balance behavior
- delays can create over-correction
- oscillation is often a feedback/delay problem
- nonlinearity creates threshold behavior
- coupling creates propagation paths
- hidden coupling creates surprising correlated failure
- critical path determines end-to-end completion
- backpressure protects constrained downstream systems
- retries can become reinforcing failure loops
- autoscaling is a feedback system
- alerts create human feedback loops
- automation creates machine feedback loops
- humans and organizational incentives are part of the system
- emergent behavior comes from interactions
- cascading failure follows dependency and feedback paths
- redundancy only helps when failure modes are independent enough
- second-order effects matter
- every intervention creates trade-offs
- leverage points can produce large system impact
- symptoms are different from system structure
- recurring incidents often reflect structural conditions
- observability should expose system relationships, not just component health
- SLOs represent system outcomes
- architecture decisions are system interventions
- more capacity, speed, retries, or redundancy are not universally beneficial

---

# 69. Practical Package — Next Layer

The practical package should include safe, provider-neutral exercises such as:

- define system boundaries for one user journey
- map components, relationships, flows, and constraints
- identify stocks and flows
- locate the active bottleneck
- compare local vs global optimization
- identify reinforcing and balancing loops
- model retry amplification
- model autoscaling delay and oscillation
- identify hidden coupling and shared failure domains
- map cascading failure
- identify second-order effects
- perform a leverage-point and intervention review

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 70. Assessment Package — Pending

The assessment should test:

- system / boundary / environment
- components / relationships / flows
- state / stock / flow
- constraints / bottlenecks
- throughput / latency / queues
- capacity / saturation
- local vs global optimization
- feedback loops
- reinforcing / balancing loops
- delays / oscillation
- nonlinearity / thresholds
- coupling / hidden coupling
- dependency chains
- critical path
- contention / backpressure
- retries as feedback
- autoscaling / alerts / automation as feedback
- human/operator loops
- incentives
- emergent behavior
- cascading failure
- blast radius / common-mode failure
- second-order effects
- trade-offs / leverage points
- symptoms vs structure
- SLOs as system outcomes
- architecture as intervention
- Senior/SRE/Architect reasoning

---

# 71. Visual Package — Pending

The visual package should include:

1. System Boundary → Components → Relationships → Flows → Outcome
2. Stock / Flow / Queue Accumulation
3. Reinforcing vs Balancing Feedback Loops
4. Local Optimization vs Global Outcome
5. Dependency Chain → Cascading Failure → Blast Radius
6. Intervention → First-Order Effect → Second-Order Effect → New System State

---

# 72. What Comes Next

After D00-T017 is completed, continue to:

## 00.18 — Failure Thinking

That topic will deepen failure modes, fault models, correlated failures, dependency failure, partial failure, degradation, overload, recovery, chaos/failure testing mental models, and failure-first architecture.

---

# 73. Sources & Evidence

Planned authoritative source families:

- systems-thinking / systems-engineering references
- Google SRE material on overload, cascading failure, retries, and reliability
- Kubernetes autoscaling / control-loop documentation
- queueing / backpressure guidance at introductory level
- cloud-provider architecture guidance on resilience and dependency behavior
- distributed-systems references for feedback and failure propagation

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: pending
- assessment package: pending
- visual package: pending

Detailed verification record:

- [D00-T017 Source Verification](../../../../docs/sources/D00/D00-T017-source-verification.md)

Verified nuances:

- a system is defined by interactions and system-level outcomes, not only by component health
- the chosen system boundary depends on the question being analyzed
- external systems, humans, policies, and interfaces may belong in the system context
- emergent behavior arises from interactions among parts
- stocks accumulate and flows change those accumulations
- reinforcing loops amplify change while balancing loops counteract deviation
- delays can create over-correction and oscillation
- local optimization can move the bottleneck or worsen the global outcome
- retries are system feedback and can amplify overload
- backpressure must propagate across upstream/downstream relationships
- autoscaling is a delayed feedback/control loop rather than instant capacity
- cascading failures commonly involve interacting conditions rather than one isolated cause
- redundancy only helps when relevant failure modes are sufficiently independent
- humans and organizational incentives can influence production-system behavior
- architecture changes are interventions whose second-order effects must be considered
