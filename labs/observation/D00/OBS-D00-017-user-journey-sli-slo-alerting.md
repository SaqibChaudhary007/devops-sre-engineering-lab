---
id: OBS-D00-017
domain: D00
topics:
  - D00-T013
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or spreadsheet optional
evidence_status:
  - DRAFT
---

# OBS-D00-017 — Map a User Journey to SLI, SLO, and Alerting Decisions

## Objective

Turn one important user journey into an SRE operating model using a service boundary, SLI, SLO, error-budget concept, and page/ticket/dashboard classification.

## Why This Matters

SRE should begin with what users need from the service, not with whichever infrastructure metric already exists.

## Safety

This is a local reasoning exercise only.

No production access, cloud account, live paging system, or disruptive testing is required.

## Scenario

Use this journey:

~~~text
Customer
→ Checkout API
→ Authentication
→ Order Service
→ Payment Provider
→ Database
~~~

The business goal is:

~~~text
Customer completes checkout correctly and within an acceptable time.
~~~

## 1. Define the Service Boundary

Write down:

- what service is being measured
- what user action defines success
- which dependencies are inside the team's operational boundary
- which dependencies are external but still affect the outcome

Explain why a poorly defined boundary can create misleading reliability metrics.

## 2. Define "Good"

Create a simple good-event definition.

Example dimensions:

- request succeeds
- payment state is correct
- order is created once
- response completes within the agreed latency threshold

Avoid defining good as:

~~~text
CPU < 70%
~~~

## 3. Design an SLI

Create one user-centered SLI.

Possible structure:

~~~text
Good Checkout Events
--------------------
Valid Checkout Events
~~~

Explain:

- numerator
- denominator
- exclusions
- what user behavior the SLI represents

## 4. Add a Latency Dimension

Design a second indicator for latency.

Example:

~~~text
Percentage of successful checkouts completed within X seconds
~~~

Explain why successful-but-slow requests can still represent poor reliability.

## 5. Define an SLO

Create a conceptual SLO for one of the SLIs.

Example structure:

~~~text
99.9% of valid checkout events are successful over a defined window
~~~

State:

- target
- window
- user journey
- what failure consumes the budget

## 6. Distinguish SLI, SLO, and SLA

Classify:

- measured checkout success ratio
- internal target for checkout success
- contractual external commitment

Explain why the three terms should not be used interchangeably.

## 7. Error-Budget Concept

Assume:

~~~text
SLO = 99.9%
~~~

Explain conceptually:

~~~text
100% - 99.9%
→ Allowed Unreliability
~~~

Then list engineering decisions the budget might influence:

- release risk
- reliability work
- investigation priority
- change pace

Do not turn one company's policy into a universal rule.

## 8. Page vs Ticket vs Dashboard

Classify each signal:

- checkout success falls sharply
- p95 checkout latency rises slightly but remains within target
- one instance restarts and service remains healthy
- error-budget consumption becomes unhealthy
- disk usage trend will become risky in several days
- payment provider is failing and checkout is blocked

Use:

~~~text
Page
Ticket
Dashboard / Context
Depends on Policy
~~~

Explain the reasoning in terms of urgency and actionability.

## 9. Symptom vs Cause

Classify:

~~~text
Checkout failure rate rising
Database pool exhausted
Payment provider timeout
CPU saturation
Users cannot complete checkout
~~~

as user-facing symptoms, technical causes, or supporting evidence.

## 10. Senior Engineer Connection

Use:

~~~text
User Journey
→ Good Event
→ SLI
→ SLO
→ Alert
→ Evidence
→ Operational Decision
~~~

## 11. SRE Connection

Explain how the same user journey connects:

~~~text
SLI
→ SLO
→ Error Budget
→ Page / Ticket / Dashboard
→ Engineering Priority
~~~

## 12. Architect Connection

Ask:

- what should the service boundary be?
- which dependency failures should consume this SLO?
- which journeys deserve their own SLO?
- what should page immediately?
- which signals belong only on dashboards?

## Validation Checklist

- [ ] Defined the service boundary
- [ ] Defined a user-centered good event
- [ ] Designed an SLI
- [ ] Designed a conceptual SLO
- [ ] Distinguished SLI/SLO/SLA
- [ ] Explained error-budget purpose
- [ ] Classified page/ticket/dashboard signals
- [ ] Distinguished symptoms from causes

## Teach-Back

Explain:

> "SRE starts with an important user journey, turns it into a measurable indicator and objective, and then uses that objective to drive operational decisions."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
