---
id: D00-T007
domain: D00
title: DevOps Foundations
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
estimated_time:
  theory: 5-7h
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
  recommended: []
evidence_status:
  - RESEARCHED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Five Levels
  - Production Room
  - Architecture With Saqib
---

# 00.07 — DevOps Foundations

## Start Here

You now understand the technical layers that applications depend on:

~~~text
Computer
→ Operating System
→ Software
→ Application Architecture
→ Infrastructure
→ Cloud
~~~

Now we connect those layers to **how engineering teams deliver change safely and repeatedly**.

The core question is:

> How do people, process, automation, architecture, and feedback work together so software can move from idea to production quickly without destroying reliability?

DevOps is not a job title, a tool, a CI/CD server, a Kubernetes cluster, or a cloud account.

DevOps is a way of improving the **flow of value and feedback** across software delivery and operations.

This topic stays at the mental-model level. Deep CI/CD, GitOps, SRE, platform engineering, observability, security, IaC, and organizational design come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- why DevOps emerged
- development vs operations responsibilities at a high level
- why organizational silos create delivery problems
- flow of work
- feedback loops
- shared ownership
- automation
- continuous integration
- continuous delivery and continuous deployment
- deployment frequency
- lead time for changes
- change failure rate
- time to restore service
- batch size
- work in progress
- handoffs
- queues
- bottlenecks
- toil
- standardization
- reproducibility
- infrastructure as code as a DevOps enabler
- observability as a feedback mechanism
- security as part of the delivery lifecycle
- shift-left and shift-right at a mental-model level
- production ownership
- blameless learning culture
- DevOps vs SRE
- DevOps vs platform engineering
- why tools do not create DevOps by themselves
- why faster delivery without feedback can increase risk
- why reliability and delivery speed are not opposites

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)
- [00.04 — Application Architecture Fundamentals](../00-04-application-architecture-fundamentals/README.md)
- [00.05 — Infrastructure Foundations](../00-05-infrastructure-foundations/README.md)
- [00.06 — Cloud Mental Models](../00-06-cloud-mental-models/README.md)

You should already understand:

- source code and artifacts
- application dependencies
- runtime and configuration
- environments
- infrastructure provisioning
- cloud APIs
- failure domains
- observability at a high level
- production risk

---

# 3. Why DevOps Exists

Traditional software delivery often separates responsibilities:

~~~text
Developers
→ write code
→ hand it over

Operations
→ deploy it
→ keep it running
~~~

This separation can create:

- slow handoffs
- conflicting incentives
- incomplete operational context
- environment drift
- delayed feedback
- unclear ownership
- repeated incidents
- "works on my machine" behavior

DevOps tries to improve the whole delivery system.

---

# 4. DevOps Is a System, Not a Team Name

A weak interpretation is:

> "We created a DevOps team, therefore we do DevOps."

A stronger model asks:

~~~text
How does work move?
How fast does feedback return?
Who owns outcomes?
What is automated?
What creates delay?
What causes failure?
How do teams learn?
~~~

A team called "DevOps" can still operate with slow tickets and silos.

A team without that title can still follow strong DevOps principles.

---

# 5. Development Perspective

Development focuses on creating and changing software.

Typical concerns include:

- features
- defects
- code quality
- dependencies
- tests
- performance
- maintainability

But software is not valuable only when committed to Git.

Value is realized when users can use the change safely.

---

# 6. Operations Perspective

Operations focuses on keeping production systems usable and recoverable.

Typical concerns include:

- availability
- capacity
- deployments
- incidents
- backups
- access
- monitoring
- recovery
- security
- change risk

Operations is not "the team that says no."

Its responsibility is to protect service outcomes.

---

# 7. Conflicting Incentives

A common failure pattern:

~~~text
Development goal
→ ship change quickly

Operations goal
→ prevent instability
~~~

If the organization optimizes each team separately:

~~~text
More changes
→ more operational fear
→ more approvals
→ slower delivery
→ larger releases
→ greater risk
~~~

DevOps aims to optimize the **system**, not one department.

---

# 8. Shared Outcomes

A DevOps-oriented organization aligns around outcomes such as:

- customer value
- reliable service
- safe change
- fast recovery
- sustainable engineering

The question changes from:

> "Whose fault is this?"

to:

> "What in the system allowed this failure, and how do we improve it?"

---

# 9. Flow

Flow describes how work moves from idea to production.

A simplified path:

~~~text
Idea
→ Plan
→ Code
→ Review
→ Build
→ Test
→ Release
→ Deploy
→ Operate
→ Learn
~~~

The goal is not to make each local step fast.

The goal is to improve the end-to-end flow.

---

# 10. Lead Time

Lead time is the time required for a change to move through the delivery system.

Conceptually:

~~~text
Change starts
     ↓
Development / Review / Test / Deploy
     ↓
Change available in production
~~~

Long lead time often indicates:

- waiting
- manual approvals
- slow tests
- large batches
- environment problems
- handoff delays

---

# 11. Batch Size

Batch size is how much change moves together.

Large batch:

~~~text
100 changes
→ one release
~~~

Small batch:

~~~text
few changes
→ frequent release
~~~

Smaller batches often make it easier to:

- review
- test
- understand
- deploy
- roll back
- identify failure causes

Small batches are not automatically safe, but they reduce the amount of change per event.

---

# 12. Work in Progress

Work in progress (WIP) means work that has started but is not finished.

Too much WIP creates:

- context switching
- queues
- waiting
- unfinished changes
- slower feedback

A team with many active items can still have poor flow.

---

# 13. Queue

A queue is waiting work.

Examples:

~~~text
PR waiting for review
ticket waiting for approval
build waiting for runner
release waiting for environment
deployment waiting for change window
incident waiting for owner
~~~

Queues hide delay.

DevOps thinking makes queues visible.

---

# 14. Handoffs

A handoff occurs when responsibility moves between people or teams.

Example:

~~~text
Developer
→ QA
→ Release Team
→ Operations
→ Security
~~~

Every handoff may introduce:

- waiting
- missing context
- misunderstanding
- rework

Not all handoffs are bad.

The goal is to reduce unnecessary handoffs and preserve useful context.

---

# 15. Bottleneck

A bottleneck limits the throughput of the whole system.

Example:

~~~text
Developers produce 20 changes/day
Release process handles 3/day
~~~

The release process is the bottleneck.

Making developers code faster does not improve end-to-end delivery.

---

# 16. Feedback Loop

A feedback loop returns information about the result of an action.

Example:

~~~text
Code Change
   ↓
Test
   ↓
Result
   ↓
Developer learns
~~~

Fast feedback helps engineers detect problems earlier.

Slow feedback allows incorrect assumptions to survive longer.

---

# 17. Feedback from Production

Production provides information that lower environments cannot fully reproduce.

Examples:

- real traffic
- real latency
- dependency behavior
- capacity pressure
- user patterns
- failure modes

This does not mean "test in production without controls."

It means production telemetry is a necessary learning signal.

---

# 18. Automation

Automation reduces repetitive manual work.

Examples:

- build
- test
- deployment
- provisioning
- configuration
- policy validation
- monitoring setup

Automation can improve:

- speed
- consistency
- repeatability
- auditability

But:

> Automation can execute a bad decision faster.

Automation requires design, testing, controls, and observability.

---

# 19. Standardization

Standardization reduces unnecessary variation.

Examples:

- common build patterns
- standard deployment interfaces
- standard logging
- standard environment naming
- reusable infrastructure modules

Standardization can reduce cognitive load.

Too much rigid standardization can block legitimate needs.

---

# 20. Reproducibility

A reproducible delivery process aims to produce predictable outcomes from known inputs.

Conceptually:

~~~text
Source
+ Dependencies
+ Build Definition
+ Configuration
→ Artifact / Environment
~~~

Reproducibility reduces:

- "works on my machine"
- undocumented steps
- environment drift
- release ambiguity

---

# 21. Continuous Integration — Mental Model

Continuous Integration (CI) means developers integrate changes frequently and validate them automatically.

Conceptually:

~~~text
Code Change
   ↓
Version Control
   ↓
Build / Test / Validation
   ↓
Fast Feedback
~~~

CI is not merely:

> "We have Jenkins/GitHub Actions/Azure DevOps."

The important idea is frequent integration plus rapid validation.

---

# 22. Continuous Delivery — Mental Model

Continuous Delivery means the software is kept in a releasable state and can be deployed through a reliable process.

Conceptually:

~~~text
Change
→ Build
→ Test
→ Package
→ Validate
→ Ready for Production
~~~

Production deployment may still require a decision or approval.

---

# 23. Continuous Deployment — Mental Model

Continuous Deployment goes further:

~~~text
Change passes required validations
→ automatically reaches production
~~~

Continuous delivery and continuous deployment are not identical.

The correct approach depends on:

- risk
- regulation
- architecture
- testing maturity
- rollback capability
- business context

---

# 24. CI/CD Is a Delivery System

A pipeline is not the goal.

The goal is:

- safe change
- fast feedback
- traceability
- repeatability
- controlled promotion
- recovery

A complex pipeline that takes hours and fails unpredictably may reduce delivery performance.

---

# 25. Deployment Frequency

Deployment frequency asks:

> How often do changes reach production?

Higher frequency can indicate smaller batches and mature delivery systems.

But frequency alone does not prove quality.

High-frequency unstable deployments are not success.

---

# 26. Change Failure Rate

Change failure rate asks:

> What proportion of production changes create degraded service and require remediation?

A change may be considered failed when it causes:

- outage
- severe degradation
- rollback
- hotfix
- emergency intervention

The exact operational definition must be explicit.

---

# 27. Time to Restore Service

Time to restore service asks:

> After service degradation, how quickly can acceptable service be restored?

Restoration may involve:

- rollback
- failover
- feature disablement
- traffic shift
- configuration change
- recovery

Fast recovery is as important as preventing every failure.

---

# 28. Delivery Performance Is Multi-Dimensional

A healthy delivery system balances:

~~~text
Speed
+ Stability
+ Recovery
+ Quality
~~~

Do not optimize only one metric.

Example:

~~~text
Deploy faster
but
fail more often
and
recover slowly
~~~

That is not good delivery performance.

---

# 29. Ownership

Ownership means teams understand and accept responsibility for the outcomes of the systems they change.

A healthy ownership model includes:

- build
- deploy
- operate
- observe
- respond
- improve

It does not mean one person must do everything.

It means responsibility does not disappear at a handoff.

---

# 30. "You Build It, You Run It" — Nuance

This phrase expresses stronger production ownership.

But organizations may implement it differently.

Possible models include:

- product teams on call
- shared SRE partnership
- centralized operations support
- platform teams providing paved roads

The goal is aligned ownership, not a slogan.

---

# 31. Toil

Toil is repetitive operational work that is manual, automatable, tactical, and does not create durable value.

Examples:

- repetitive deployment steps
- repeated user creation
- manual log collection
- repeated environment repair

Not every manual task is toil.

Some manual work requires judgment.

---

# 32. Reduce Toil, Preserve Judgment

The goal is not:

> automate humans away.

The goal is:

~~~text
Automate repetitive work
→ free time for engineering
→ improve systems
→ reduce future toil
~~~

Human judgment remains important for:

- architecture
- incident decisions
- risk
- exceptions
- trade-offs

---

# 33. Infrastructure as Code as a DevOps Enabler

IaC supports DevOps by making infrastructure:

- versionable
- reviewable
- repeatable
- automatable
- easier to compare

Conceptually:

~~~text
Infrastructure Change
→ Code Review
→ Automated Validation
→ Apply
→ Observe
~~~

IaC is an enabler, not DevOps itself.

---

# 34. Observability as Feedback

Observability closes the production feedback loop.

Conceptually:

~~~text
Deploy
  ↓
Production Behavior
  ↓
Metrics / Logs / Traces / Events
  ↓
Learn
  ↓
Improve
~~~

Without production feedback, delivery teams can ship changes without understanding outcomes.

---

# 35. Security in the Delivery Flow

Security should not be only a final gate.

Security concerns can appear during:

- design
- coding
- dependency selection
- build
- artifact handling
- infrastructure provisioning
- deployment
- runtime

This is often described as integrating security into the lifecycle.

---

# 36. Shift Left — Mental Model

Shift left means moving useful validation earlier in the lifecycle.

Examples:

- tests before merge
- dependency scanning during build
- policy validation before deploy
- configuration checks before production

Goal:

> detect problems earlier when they are cheaper and easier to fix.

---

# 37. Shift Right — Mental Model

Shift right means learning from runtime/production behavior.

Examples:

- production telemetry
- feature flags
- canary analysis
- runtime security
- chaos/reliability experiments
- user feedback

Shift left and shift right are complementary.

---

# 38. Environment Parity

If environments differ too much:

~~~text
Test passes
→ production fails
~~~

Potential differences include:

- configuration
- dependency versions
- network
- data
- permissions
- scale

Perfect parity is often impossible.

The goal is to reduce uncontrolled differences and understand the remaining ones.

---

# 39. Configuration Management

Applications depend on configuration such as:

- endpoints
- credentials
- feature flags
- resource limits
- timeouts
- environment settings

Configuration should be:

- controlled
- traceable
- appropriately separated from code
- secure where sensitive

Uncontrolled configuration change can cause incidents without code changes.

---

# 40. Change Management

Every production change introduces risk.

Good change management asks:

~~~text
What is changing?
Why?
How was it validated?
Who owns it?
What is the blast radius?
How do we detect failure?
How do we recover?
~~~

DevOps does not mean "no change controls."

It means controls should be proportional, evidence-driven, and automation-friendly where possible.

---

# 41. Deployment Strategies — Preview

Different deployment strategies reduce risk in different ways.

Examples:

- rolling
- blue/green
- canary
- feature flags

At D00 level, retain:

> Deployment design can reduce blast radius and improve recovery.

Deep implementation comes later.

---

# 42. Rollback and Roll Forward

When a change fails, teams may:

- roll back to a previous known version
- roll forward with a corrective change

The correct choice depends on:

- data changes
- compatibility
- deployment speed
- risk
- failure mode

Recovery must be designed before the incident.

---

# 43. Blameless Learning

Blameless does not mean:

> no accountability.

It means incident learning avoids stopping at:

> "A person made a mistake."

Instead ask:

- why was the action possible?
- what information was missing?
- what guardrail failed?
- what pressure existed?
- what detection was absent?
- how can recurrence be reduced?

---

# 44. Incident Feedback Loop

An incident can produce:

~~~text
Detection
→ Response
→ Recovery
→ Analysis
→ Action Items
→ System Improvement
~~~

If incidents create no durable learning, the organization repeats failure.

---

# 45. DevOps and Reliability

Speed and reliability are not necessarily opposites.

Good delivery systems can improve both through:

- smaller batches
- automation
- fast feedback
- reproducibility
- observability
- rollback
- controlled exposure

Large risky releases are often a symptom of slow delivery systems.

---

# 46. DevOps vs SRE

DevOps is a broad philosophy and operating model for improving delivery and operations.

SRE applies software-engineering approaches to reliability.

A useful mental model:

~~~text
DevOps
→ principles for flow, feedback, collaboration, automation

SRE
→ reliability-focused implementation discipline
~~~

They overlap.

They are not identical.

---

# 47. DevOps vs Platform Engineering

Platform engineering focuses on building internal products/platforms that improve developer experience and operational consistency.

Conceptually:

~~~text
DevOps principles
      ↓
Platform capabilities / paved roads
      ↓
Teams deliver with less cognitive load
~~~

Platform engineering can enable DevOps.

It does not replace the need for shared ownership and feedback.

---

# 48. DevOps vs Tools

Tools may include:

- Git
- CI/CD platforms
- containers
- Kubernetes
- cloud
- Terraform
- Ansible
- observability systems

But owning these tools does not prove DevOps maturity.

Ask instead:

~~~text
Is delivery faster?
Is feedback faster?
Are failures safer?
Is recovery faster?
Is work more repeatable?
Are teams learning?
~~~

---

# 49. DevOps Anti-Patterns

Common anti-patterns include:

## DevOps as a Ticket Team

~~~text
Developer
→ DevOps ticket
→ deployment
~~~

The handoff remains.

## Automation Without Ownership

~~~text
Pipeline exists
→ nobody understands production outcome
~~~

## Tool-First Transformation

~~~text
Buy tools
→ culture/process unchanged
~~~

## One Giant Pipeline

~~~text
every service
→ one fragile release process
~~~

## Speed Without Safety

~~~text
deploy more often
→ no testing / no observability / no rollback
~~~

---

# 50. Senior Engineer Perspective

A senior engineer asks:

- where is delivery time spent?
- where does work wait?
- what is manual?
- what is fragile?
- what is hard to reproduce?
- what is the rollback path?
- what telemetry proves success?
- what dependency slows delivery?
- where is ownership unclear?

The senior view is end-to-end, not tool-by-tool.

---

# 51. SRE Perspective

An SRE asks:

- how does deployment affect SLOs?
- which changes correlate with incidents?
- how quickly can service recover?
- what is the change failure rate?
- how much operational toil exists?
- are alerts actionable?
- can the system degrade safely?
- is release risk bounded?

SRE connects delivery practices to reliability outcomes.

---

# 52. Architect Perspective

An architect asks:

- what delivery model fits the system?
- what is the acceptable change risk?
- what compliance requirements exist?
- how independent are components?
- what must be standardized?
- where is team autonomy valuable?
- what platform capability is reusable?
- which controls should be automated?
- what deployment strategy fits the data model?

Architecture includes the path to production, not only runtime diagrams.

---

# 53. Common Beginner Mistakes

## Mistake 1

"DevOps is a tool."

No. Tools can support DevOps practices.

## Mistake 2

"DevOps means developers do operations alone."

No. The goal is shared outcomes and better flow, not eliminating specialized expertise.

## Mistake 3

"CI/CD means we installed Jenkins."

No. The important outcomes are frequent integration, reliable validation, safe promotion, and feedback.

## Mistake 4

"More automation always means better DevOps."

Bad automation can scale bad decisions.

## Mistake 5

"Faster deployments reduce reliability."

Poorly controlled change can reduce reliability; small, observable, recoverable changes can improve both speed and reliability.

## Mistake 6

"Blameless means nobody is accountable."

Blameless learning focuses on improving systems while still expecting responsible engineering behavior.

## Mistake 7

"Platform engineering replaces DevOps."

Platform engineering can operationalize many DevOps principles, but does not replace ownership, feedback, or collaboration.

---

# 54. Five-Level Explanation

## L1 — Foundation

DevOps helps software teams build, deliver, operate, and improve software together.

## L2 — Engineer

DevOps improves delivery through automation, shared ownership, smaller changes, fast feedback, and repeatable processes.

## L3 — Senior Engineer

DevOps is an end-to-end system of flow, feedback, architecture, automation, ownership, and recovery—not a collection of tools.

## L4 — SRE

Delivery performance must be evaluated against reliability, failure rate, recovery speed, toil, and user-facing outcomes.

## L5 — Architect

DevOps architecture aligns organizational design, delivery systems, platform capabilities, governance, reliability, and technical boundaries so change can flow safely at scale.

---

# 55. What You Must Retain

Before moving on, retain:

- DevOps optimizes the delivery system, not one team
- flow and feedback are central
- queues, handoffs, large batches, and WIP slow delivery
- automation improves repeatability but can automate mistakes
- CI is frequent integration plus validation
- continuous delivery and continuous deployment are different
- deployment frequency alone does not prove maturity
- change failure and recovery matter
- production telemetry is part of the feedback loop
- shared ownership matters
- toil should be reduced through engineering
- IaC, observability, security, and platform engineering can enable DevOps
- shift-left and shift-right are complementary
- environment/configuration differences can create risk
- change management should be proportional and evidence-driven
- recovery should be designed before failure
- blameless learning focuses on system improvement
- DevOps, SRE, and platform engineering overlap but are not identical
- tools do not prove DevOps maturity

---

# 56. Practical Package — Next Layer

The practical package should include safe exercises such as:

- map one feature from idea → code → review → build → test → deploy → operate → learn
- identify queues, handoffs, WIP, and bottlenecks in a hypothetical delivery system
- compare one large release with multiple smaller releases
- design a basic feedback loop using build/test/deployment/production signals
- classify repetitive operational work as toil vs judgment work
- build a lightweight delivery-metrics worksheet

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 57. Assessment Package — Pending

The assessment should test:

- why DevOps exists
- flow
- feedback
- WIP
- queues
- handoffs
- bottlenecks
- automation
- standardization
- CI/CD mental models
- deployment/recovery metrics
- ownership
- toil
- observability
- security integration
- shift left/right
- change management
- DevOps vs SRE vs platform engineering
- Senior/SRE/Architect reasoning

---

# 58. Visual Package — Pending

The visual package should include:

1. Traditional Siloed Delivery vs DevOps Flow
2. Idea → Production → Feedback Loop
3. Queue / Handoff / Bottleneck Model
4. CI vs Continuous Delivery vs Continuous Deployment
5. Delivery Performance: Speed / Stability / Recovery
6. DevOps vs SRE vs Platform Engineering

---

# 59. What Comes Next

After D00-T007 is completed, continue to:

## 00.08 — Infrastructure as Code Mental Model

That topic will connect DevOps delivery principles to:

- desired state
- declarative vs imperative approaches
- version-controlled infrastructure
- repeatability
- drift
- plan/apply lifecycle
- state
- review
- automation

---

# 60. Sources & Evidence

Planned authoritative source families for verification:

- Google Cloud / DORA research and delivery-performance guidance
- DevOps Handbook references where appropriate
- Google SRE material
- Microsoft/AWS/Google engineering guidance on CI/CD
- CNCF/platform-engineering material
- NIST/OWASP/official security guidance for lifecycle integration
- authoritative incident-learning and operations references

Current evidence status:

- conceptual draft: RESEARCHED
- source verification: pending
- practical package: pending
- assessment package: pending
- visual package: pending
