---
id: EXP-D00-030
domain: D00
topics:
  - D00-T017
level: L2-L3
type: experiment
status: draft
estimated_time: 60-80m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-030 — Hidden Coupling, Cascading Failure, Second-Order Effects, and Leverage Points

## Objective

Practice finding hidden dependencies, common-mode failure, cascading-failure paths, second-order effects, and high-leverage interventions.

## Safety

This is a reasoning and architecture exercise only.

Do not disable dependencies, simulate outages on shared systems, or perform destructive failure injection.

## Scenario

Three business services appear independent:

~~~text
Checkout Service
Inventory Service
Notification Service
~~~

But all three share:

- one database cluster
- one cloud IAM quota
- one DNS resolver path
- one deployment pipeline
- one on-call team

Checkout also depends on an external payment provider.

## 1. Map Visible Coupling

Draw the obvious dependencies between:

- user
- checkout
- inventory
- notification
- database
- payment provider

## 2. Find Hidden Coupling

Add the shared:

- IAM quota
- DNS path
- deployment pipeline
- on-call team

Explain why components that look independent can still fail together.

## 3. Identify Common Failure Domains

Classify shared dependencies as possible common-mode failure domains.

Ask:

- what if the database cluster fails?
- what if IAM quota is exhausted?
- what if DNS breaks?
- what if the deployment pipeline pushes bad config everywhere?
- what if the on-call team is overloaded?

## 4. Map Cascading Failure

Use this example:

~~~text
Payment slows
→ Checkout latency rises
→ Client retries rise
→ Database sessions rise
→ Connection pool saturates
→ Inventory requests slow
→ Queue backlog grows
→ Alert volume rises
→ On-call cognitive load rises
~~~

Identify:

- initiating condition
- propagation path
- reinforcing feedback
- human-system interaction
- user impact

## 5. Blast-Radius Review

For each shared dependency, ask:

~~~text
If this fails, what fraction of the system is affected?
~~~

Then propose architectural ways to reduce blast radius conceptually.

Examples:

- isolation
- independent failure domains
- scoped credentials
- separate pipelines
- rate limits
- graceful degradation

## 6. Redundancy Review

Review this statement:

~~~text
"We have two replicas, so we are redundant."
~~~

Ask whether the replicas still share:

- database
- region
- credentials
- control plane
- network path

Explain why redundancy and independence are different.

## 7. First-Order Effect

Intervention:

~~~text
Add Cache
~~~

Expected first-order effect:

~~~text
Database load decreases
~~~

## 8. Second-Order Effects

Now ask what happens next:

- traffic capacity rises
- payment traffic rises
- cache invalidation complexity increases
- stale-data risk changes
- downstream bottleneck may move

Explain why successful interventions can create new system behavior.

## 9. Leverage-Point Review

Compare possible interventions:

- add API CPU
- increase retry count
- reduce duplicate work
- improve backpressure
- isolate shared dependency
- change timeout policy
- improve queue admission

Rank them by likely system leverage.

Explain your assumptions.

## 10. Symptoms vs Structure

Symptom:

~~~text
High Checkout Latency
~~~

Possible structure:

~~~text
Shared Dependency
+ Unbounded Retry
+ No Backpressure
+ Slow Feedback
+ One On-Call Team
~~~

Explain why treating only the symptom may cause recurrence.

## 11. Event → Pattern → Structure → Policy

Use:

~~~text
Event:
Checkout outage

Pattern:
Outages happen during payment slowdown

Structure:
Retries + shared DB + no backpressure

Policy / Mental Model:
"Retry more to improve reliability"
~~~

Explain how deeper layers suggest stronger interventions.

## 12. SLO as System Outcome

Map which relationships influence:

~~~text
Checkout SLO
~~~

Include:

- API
- database
- payment
- queue
- capacity
- deployment safety
- human response

## 13. Senior Engineer Connection

Use:

~~~text
Symptom
→ Dependency Map
→ Hidden Coupling
→ Propagation Path
→ Feedback
→ Structural Cause
→ Intervention
~~~

## 14. SRE Connection

Connect:

- common-mode failure
- overload
- retry storms
- incident patterns
- SLOs
- alert fatigue
- recovery

## 15. Architect Connection

Decide:

- what should be isolated
- where redundancy needs true independence
- what coupling is acceptable
- which intervention has highest leverage
- what second-order behavior could appear after success

## Validation Checklist

- [ ] Mapped visible dependencies
- [ ] Identified hidden coupling
- [ ] Identified common failure domains
- [ ] Mapped a cascading-failure path
- [ ] Reviewed blast radius
- [ ] Distinguished redundancy from independence
- [ ] Identified first-order effects
- [ ] Identified second-order effects
- [ ] Ranked leverage points
- [ ] Distinguished symptoms from structure
- [ ] Used event → pattern → structure → policy reasoning
- [ ] Connected the system to an SLO

## Teach-Back

Explain:

> "The highest-leverage fix often comes from changing a relationship, feedback loop, or shared dependency rather than making one component faster."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
