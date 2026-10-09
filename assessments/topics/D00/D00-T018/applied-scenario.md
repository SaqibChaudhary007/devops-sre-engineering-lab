# D00-T018 — Applied Failure Thinking Scenario

## Scenario

A checkout platform uses:

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

Shared dependencies:

~~~text
- one DNS path
- one database cluster
- one identity system
- one deployment pipeline
- one on-call team
~~~

Observed behavior:

~~~text
- payment latency rises from 200 ms to 8 seconds
- API CPU remains moderate
- DB connections approach saturation
- checkout timeouts increase
- retry volume increases
- queue age rises
- health checks remain green in some regions
- users report duplicate payment attempts
- autoscaling adds API replicas after a delay
- secondary region exists but has not been tested recently
- backups complete daily, but restore testing has not occurred in months
~~~

## Task 1 — Failure Classification

Identify:

- initiating fault/stressor
- internal degraded states
- externally visible failures
- user/business impact

## Task 2 — Failure Modes

Classify the payment dependency across:

- slow
- intermittent
- partial
- transient vs non-transient
- state uncertainty

Explain what evidence is still missing.

## Task 3 — Failure Domains

Map possible failure domains for:

- database
- payment provider
- DNS
- identity system
- deployment pipeline
- secondary region

## Task 4 — Blast Radius

Estimate the conceptual blast radius of each shared dependency.

Explain what would make the estimate uncertain.

## Task 5 — Retry Amplification

Map:

~~~text
Client Retry
+ Gateway Retry
+ Service Retry
→ More Payment Calls
→ More Waiting
→ More DB Connection Occupancy
→ Wider Failure
~~~

Explain how retry ownership should be simplified or bounded.

## Task 6 — Timeout Boundaries

Map timeout budgets across:

~~~text
Client
→ Gateway
→ Checkout
→ Payment Client
→ Payment Provider
~~~

Explain why inner timeouts should not exceed the useful outer budget.

## Task 7 — Backpressure and Load Shedding

Design a conceptual overload response using:

- reduced admission
- backpressure
- bounded queueing
- optional-feature shedding
- graceful degradation

## Task 8 — Critical vs Optional Dependencies

Classify:

- payment
- recommendations
- notifications
- analytics
- audit event

Explain which can degrade and which cannot.

## Task 9 — Redundancy vs Independence

Review the secondary region and identify shared dependencies that could still defeat failover.

## Task 10 — Failover Readiness

List failover preconditions:

- detection
- capacity
- routing
- state
- configuration
- credentials
- dependency health
- runbook
- operator readiness

## Task 11 — Backup vs Recovery

Explain why:

~~~text
Backup Job = Successful
~~~

does not prove:

~~~text
Business Service = Recoverable
~~~

Define a restore-validation plan.

## Task 12 — RTO / RPO

Explain what business questions must be answered before choosing:

- RTO
- RPO

## Task 13 — State Uncertainty

Scenario:

~~~text
Payment request sent
→ caller times out
→ outcome unknown
~~~

Explain why blind retry may be unsafe.

Propose evidence required for reconciliation.

## Task 14 — Containment

Rank safe conceptual containment actions:

- pause nonessential traffic
- reduce retries
- shed lower-priority work
- disable optional features
- pause deployment
- isolate failing path

Explain why containment can come before complete RCA.

## Task 15 — Recovery Validation

After mitigation, validate:

- user-facing success
- p95 latency
- error rate
- retry rate
- queue age
- DB connection utilization
- duplicate-processing rate
- payment correctness
- regional health
- security/identity state

## Task 16 — Pre-Mortem

Imagine failover failed badly.

List likely conditions that caused it and convert them into readiness checks.

## Task 17 — Safe Failure-Test Design

Create a tabletop or non-production experiment with:

- hypothesis
- environment
- scope
- expected steady state
- controlled disturbance
- observability
- stop conditions
- recovery plan
- owner/authorization
- validation

Do not propose uncontrolled production disruption.

## Task 18 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Failure Mode
→ Propagation
→ State Uncertainty
→ Containment
→ Recovery
→ Validation
~~~

### SRE

Connect:

- SLO impact
- retry amplification
- overload
- graceful degradation
- restore readiness
- game days
- operational evidence

### Architect

Redesign:

- failure domains
- dependency criticality
- retry ownership
- failover topology
- recovery objectives
- shared/common-mode dependencies
- validation strategy

## Success Standard

A strong answer should explicitly reject:

- complete outage = only failure
- more retries = automatic reliability
- replicas = guaranteed independence
- failover = guaranteed recovery
- backup success = recovery proven
- green health checks = healthy users
- one metric green = recovery complete
- chaos engineering = random destruction
