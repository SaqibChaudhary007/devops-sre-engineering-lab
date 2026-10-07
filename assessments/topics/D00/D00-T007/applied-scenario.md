# D00-T007 — Applied Delivery-System Scenario

## Scenario

A product team releases a customer-facing API every two weeks.

Current delivery flow:

~~~text
Idea
→ Development
→ Code Review
→ Build
→ QA
→ Security Review
→ Change Approval
→ Production Deployment
→ Operations
~~~

Observed facts:

~~~text
Developers complete coding quickly.
PRs wait 8–16 hours for review.
QA environment is shared by five teams.
Builds wait for available runners.
Security review begins only after QA.
Production deployments happen every second Friday.
Average release contains 35–50 changes.
Rollback is manual.
Production telemetry is owned only by Operations.
Developers rarely join incident reviews.
Two recent releases required emergency corrective deployments.
Change approval frequently waits one business day.
~~~

Current weekly metrics:

~~~text
Deployment frequency: low
Change lead time: high
Failed deployment recovery time: high
Change fail rate: rising
Deployment rework rate: rising
~~~

## Task 1 — Map the Delivery System

Draw the end-to-end flow and identify:

- active work
- queues
- handoffs
- bottlenecks
- feedback loops
- missing feedback loops

## Task 2 — Find the Largest Sources of Delay

Rank at least five delay sources.

Do not answer only with "developers need to work faster."

Explain why local coding speed is not the current system constraint.

## Task 3 — Batch Size

Explain how a two-week release window produces larger batches.

Discuss the effect on:

- review
- testing
- debugging
- rollback
- change fail rate
- recovery
- context

## Task 4 — CI/CD Reasoning

Evaluate the statement:

> "We already have CI/CD because we use a pipeline."

Explain what additional evidence would be needed to prove strong CI/CD practice.

Consider:

- integration frequency
- test speed
- pipeline reliability
- promotion flow
- release readiness
- production feedback
- recovery

## Task 5 — DORA Metrics

Explain what each current DORA metric reveals about this delivery system:

- change lead time
- deployment frequency
- failed deployment recovery time
- change fail rate
- deployment rework rate

Then explain why none should be optimized alone.

## Task 6 — Ownership

Production telemetry is owned only by Operations.

Explain:

- what feedback developers are missing
- how this affects learning
- how shared ownership could improve the loop
- why shared ownership does not mean removing operations expertise

## Task 7 — Toil

Identify likely toil in the scenario.

Potential candidates:

- manual rollback
- repeated change-window coordination
- repeated environment reset
- manual evidence collection

For each, propose an engineering improvement.

## Task 8 — Shift Left / Shift Right

Security starts only after QA.

Propose a better lifecycle model that includes both:

- earlier useful validation
- runtime/production feedback

Do not move every control left blindly.

## Task 9 — Incident Learning

Developers rarely join incident reviews.

Explain why this weakens the feedback loop.

Design a simple incident-learning cycle:

~~~text
Detect
→ Respond
→ Recover
→ Analyze
→ Action
→ Improve
~~~

## Task 10 — Senior Engineer Response

Write a prioritized improvement plan.

Use:

~~~text
Measure Flow
→ Reduce Queueing
→ Reduce Batch Size
→ Improve Fast Feedback
→ Automate Repetitive Work
→ Improve Recovery
→ Share Production Feedback
→ Measure Outcomes
~~~

## Task 11 — SRE View

Explain how delivery practices affect:

- SLOs
- alert volume
- incident frequency
- failed deployment recovery time
- operational toil
- blast radius

## Task 12 — Architect View

Design a target delivery model that balances:

- team autonomy
- platform standardization
- security
- compliance
- release safety
- observability
- rollback/recovery
- developer experience

Do not solve the problem by simply saying:

> "Buy a new CI/CD tool."

## Success Standard

A strong response identifies the system problem rather than blaming one team.

It should clearly connect:

- queues
- handoffs
- batch size
- feedback
- ownership
- toil
- DORA metrics
- recovery

and propose improvements that reduce lead time without weakening reliability.
