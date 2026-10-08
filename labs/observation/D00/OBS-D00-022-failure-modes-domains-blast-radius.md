---
id: OBS-D00-022
domain: D00
topics:
  - D00-T018
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# OBS-D00-022 — Failure Modes, Failure Domains, and Blast Radius

## Objective

Practice identifying how a system can fail, how failure differs from a fault or internal error, where failures can be correlated, and how far impact can spread.

## Why This Matters

A useful failure review does not stop at:

> "The service went down."

It asks:

~~~text
What failed?
How did it fail?
What became incorrect internally?
What did users observe?
What shared dependency was involved?
How far could the impact spread?
~~~

## Safety

This is a local reasoning exercise only.

Do not disable services, remove infrastructure, exhaust resources, or intentionally disrupt production systems.

## Scenario

Use this user journey:

~~~text
Customer
→ DNS
→ Load Balancer
→ API
→ Authentication
→ Order Service
→ Database
→ Payment Provider
→ Queue
→ Worker
~~~

Shared platform dependencies:

~~~text
- one DNS path
- one database cluster
- one secrets/identity system
- one deployment pipeline
- one on-call team
~~~

## 1. Distinguish Fault, Error, Failure, and Impact

For each case, identify:

- fault / stressor
- incorrect internal state or degradation
- externally visible failure
- user/business/system impact

Cases:

1. database becomes unreachable
2. payment provider becomes very slow
3. stale configuration is loaded
4. certificate expires
5. worker processes the same message twice

## 2. Classify Failure Modes

For each component, consider whether it can fail by being:

- unavailable
- slow
- intermittent
- stale
- incorrect
- partially reachable
- duplicated
- accepting work but never finishing

Explain why "up/down" is too narrow.

## 3. Classify Failure Duration / Behavior

Classify scenarios as:

~~~text
Transient
Permanent / Non-Transient
Intermittent
Partial / Degraded
Needs More Evidence
~~~

Examples:

- brief packet loss
- revoked credential
- one unhealthy zone
- invalid configuration
- API that fails 1 request in 20
- dependency that responds in 20 seconds instead of 200 ms

## 4. Map Failure Domains

For each dependency, identify its possible failure domain:

- process
- host
- node
- zone
- region
- account/project
- database cluster
- identity system
- deployment pipeline
- human/operator path

## 5. Hidden Shared Dependencies

Add the shared:

- DNS
- database
- identity system
- deployment pipeline
- on-call team

Explain why apparently redundant services can still fail together.

## 6. Blast-Radius Review

For each scenario, estimate conceptual blast radius:

~~~text
One Request
One Instance
One Service
One Tenant
One Zone
One Region
Whole Platform
~~~

Explain what evidence is needed before claiming the true blast radius.

## 7. Redundancy vs Independence

Review:

~~~text
"We have three replicas, so this service is resilient."
~~~

Check whether all replicas share:

- same database
- same zone
- same secret
- same control plane
- same deployment
- same operator action

Explain why replica count is not the same as failure independence.

## 8. Critical vs Degradable Dependency

Classify dependencies as:

~~~text
Critical
Degradable
Optional
Asynchronous
~~~

Example:

- payment provider
- recommendation service
- audit pipeline
- notification worker

Explain how this classification affects failure behavior.

## 9. Slow Failure Chain

Model:

~~~text
Payment Slows
→ Requests Wait
→ Connections Stay Occupied
→ Timeouts Rise
→ Retries Rise
→ More Load
→ Wider Impact
~~~

Identify where containment could interrupt propagation.

## 10. Gray / Observer-Dependent Failure

Consider:

~~~text
Health Check = Green
User Requests = Failing
~~~

List possible reasons why observers disagree.

## 11. Senior Engineer Connection

Use:

~~~text
Assumption
→ Failure Mode
→ Internal Degradation
→ Observable Impact
→ Failure Domain
→ Blast Radius
→ Containment
~~~

## 12. SRE Connection

Connect to:

- SLO impact
- detection gaps
- dependency health
- retries
- saturation
- alerting
- mitigation priority

## 13. Architect Connection

Ask:

- which failure domains are truly independent?
- which shared dependencies create common-mode risk?
- which user journeys need graceful degradation?
- what blast radius is acceptable?
- what should be isolated?

## Validation Checklist

- [ ] Distinguished fault, internal degradation, failure, and impact
- [ ] Identified multiple failure modes
- [ ] Classified transient/permanent/intermittent/partial behavior
- [ ] Mapped failure domains
- [ ] Identified hidden shared dependencies
- [ ] Estimated blast radius
- [ ] Distinguished redundancy from independence
- [ ] Classified critical vs degradable dependencies
- [ ] Modeled a slow-failure propagation chain
- [ ] Explained observer-dependent / gray behavior

## Teach-Back

Explain:

> "Failure thinking is not just asking whether a component is up or down; it is identifying how it can fail, how impact propagates, and how much of the system shares the same failure domain."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
