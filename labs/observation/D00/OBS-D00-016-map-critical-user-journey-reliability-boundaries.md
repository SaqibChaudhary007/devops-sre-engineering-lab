---
id: OBS-D00-016
domain: D00
topics:
  - D00-T012
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

# OBS-D00-016 — Map a Critical User Journey and Reliability Boundaries

## Objective

Build a user-centered reliability model by tracing one important service journey from user action through dependencies, failure domains, and observable outcomes.

## Why This Matters

A platform can report healthy infrastructure while a critical user journey is broken.

Reliability should therefore begin with:

> What must the user be able to do successfully?

## Safety

This is a local reasoning exercise only.

No production access, cloud account, destructive action, or live failure injection is required.

## Scenario

Use this critical user journey:

~~~text
Customer
→ DNS
→ Load Balancer
→ Web/API
→ Authentication
→ Order Service
→ Database
→ Payment Provider
→ Queue
→ Fulfillment Worker
~~~

The user goal is:

~~~text
Place an order successfully
~~~

## 1. Define Success

Write a user-centered success condition for the order journey.

Include:

- request succeeds
- response is timely enough
- order state is correct
- payment state is correct
- fulfillment work is accepted

Avoid defining success as:

~~~text
All servers are up
~~~

## 2. Map Critical Dependencies

For each component, classify:

~~~text
Critical
Degradable
Optional
Unknown
~~~

Ask:

- if this dependency fails, does checkout fail?
- can the system continue in reduced mode?
- can work be deferred?
- is there a fallback?

## 3. Availability vs Reliability

For each case, decide whether the service is:

~~~text
Available but Unreliable
Unavailable
Reliable
Partially Degraded
~~~

Cases:

- checkout responds 200 but creates duplicate orders
- checkout succeeds but takes 45 seconds
- recommendation panel is unavailable but order succeeds
- payment succeeds but confirmation is lost
- database is healthy but authentication is down

## 4. Failure Domains

Map likely failure domains:

- process
- node
- zone
- region
- database
- external provider
- identity provider
- queue
- shared network path

Explain which failures could affect multiple components together.

## 5. Blast Radius

For each failure, estimate impact:

~~~text
One request
One tenant
One component
One zone
All users
~~~

Failures:

- one API process exits
- one zone loses connectivity
- payment provider is unavailable
- identity provider fails
- queue backlog grows for one tenant

## 6. Graceful Degradation

Choose which capabilities can be degraded safely:

- recommendations
- order history
- promotional banner
- payment
- inventory validation
- shipping estimate

Explain why some features can be removed temporarily while others are correctness-critical.

## 7. Reliability Evidence

For the end-to-end order journey, identify useful evidence:

- request success ratio
- p95 latency
- payment errors
- queue age
- authentication errors
- database saturation
- dependency health
- deployment markers

## 8. Senior Engineer Connection

Use:

~~~text
User Journey
→ Success Criteria
→ Critical Dependencies
→ Failure Domains
→ Blast Radius
→ Degradation Options
→ Evidence
~~~

## 9. SRE Connection

Connect the user journey to:

- availability
- latency
- error rate
- freshness/correctness
- SLO thinking
- alerting priority

## 10. Architect Connection

Ask:

- which dependencies dominate reliability?
- where should redundancy exist?
- which failure domains must be independent?
- where can graceful degradation be introduced?
- what should be measured end to end?

## Validation Checklist

- [ ] Defined user-centered success
- [ ] Mapped critical dependencies
- [ ] Distinguished availability from broader reliability
- [ ] Mapped failure domains
- [ ] Estimated blast radius
- [ ] Designed graceful degradation
- [ ] Identified end-to-end reliability evidence

## Teach-Back

Explain:

> "Reliability begins with the critical user journey, not with whether individual infrastructure components look healthy."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
