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
- one managed database cluster
- one identity/secrets system
- one deployment pipeline
- one on-call team
~~~

Observed incident:

~~~text
- payment latency rises from 200 ms to 8 seconds
- API CPU remains moderate
- database connections approach saturation
- checkout timeouts increase
- clients retry
- queue depth remains mostly stable
- oldest-message age increases
- some health checks stay green
- users report failed or duplicated checkout attempts
- alert volume increases sharply
- the secondary region exists but has not been failover-tested recently
- backups report successful completion
~~~

## Task 1 — Define Fault, Error, Failure, Impact

Identify:

- initiating fault/stressor
- internal degraded state
- externally visible failure modes
- user/business impact

## Task 2 — Classify Failure Modes

Classify the incident across:

- slow
- partial
- intermittent
- observer-dependent / gray
- overload-related
- state-uncertain

Explain which labels are strongly supported vs still uncertain.

## Task 3 — Map Failure Domains

Identify possible failure domains:

- payment provider
- database cluster
- DNS
- identity
- deployment pipeline
- region
- on-call team

Explain which are shared/common-mode risks.

## Task 4 — Blast Radius

Estimate conceptual blast radius at:

~~~text
Request
Service
Tenant
Zone
Region
Platform
~~~

Explain what evidence is required before claiming the real blast radius.

## Task 5 — Dependency Criticality

Classify:

- payment
- recommendations
- notifications
- analytics
- audit pipeline

as:

~~~text
Critical
Degradable
Optional
Asynchronous
~~~

Explain the effect on failure behavior.

## Task 6 — Timeout Boundaries

Map:

~~~text
Client
→ Gateway
→ Checkout
→ Payment Client
→ Payment Provider
~~~

Explain how badly composed timeouts can leave work running after callers have already given up.

## Task 7 — Retry Amplification

Model how retries across:

- client
- gateway
- service

could amplify payment load.

Then define what evidence would justify retry vs no-retry.

## Task 8 — Backpressure and Load Shedding

Design a conceptual overloaded-state policy:

- what signal indicates saturation?
- what work can be rejected?
- what work can be deferred?
- what work must remain protected?
- how should upstream callers react?

## Task 9 — Graceful Degradation

Choose features that can be disabled or skipped without invalidating checkout correctness.

Explain why degradation requires product/business understanding.

## Task 10 — Circuit-Breaker Applicability

Explain whether a circuit breaker could help the payment dependency.

Also identify cases where:

- queueing
- isolation
- rate limiting
- direct failure
- provider-side recovery

might be more appropriate.

## Task 11 — Redundancy vs Independence

Review:

~~~text
"We have multiple API replicas and a secondary region, so we are resilient."
~~~

Check whether they still share:

- database
- identity
- DNS/control path
- deployment pipeline
- artifact source
- operator process

## Task 12 — Failover Readiness

List failover assumptions:

- detection
- capacity
- routing
- data freshness
- credentials
- dependency health
- runbook
- ownership

Identify what is unproven.

## Task 13 — Backup vs Recovery

Given:

~~~text
Backup job = successful
~~~

Explain what additional evidence is needed to prove recoverability.

## Task 14 — RTO / RPO

Translate:

~~~text
"Recovery should be fast."
"Data loss should be minimal."
~~~

into the correct business questions.

Explain why engineering cannot choose the targets alone.

## Task 15 — State Uncertainty

Scenario:

~~~text
Payment request sent
→ caller times out
→ duplicate checkout attempt arrives
~~~

Explain how:

- operation ID
- idempotency key
- status lookup
- audit trail
- reconciliation

can reduce duplicate side effects.

## Task 16 — Partition / Quorum Preview

Explain why:

~~~text
Network partition
→ authority/availability decision
~~~

and why exact behavior must remain protocol-specific.

## Task 17 — Containment

Choose the fastest safe containment options from:

- pause rollout
- reduce retries
- shed lower-priority work
- isolate degraded path
- disable optional feature
- reduce admission

Explain why containment can come before full RCA.

## Task 18 — Recovery Validation

After payment latency improves, define evidence for real recovery:

- user-facing success
- latency
- error rate
- retries
- queue age
- database connections
- data correctness
- dependency health
- security/identity state

## Task 19 — Pre-Mortem / Game Day

Design a tabletop scenario for:

~~~text
Primary region unavailable while shared identity is degraded
~~~

Include:

- expected behavior
- decision points
- failover criteria
- stop conditions
- validation
- communication
- lessons learned

## Task 20 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Failure Mode
→ Propagation
→ State
→ Blast Radius
→ Containment
→ Recovery
→ Validation
~~~

### SRE

Connect:

- SLO impact
- retry amplification
- overload protection
- alert quality
- mitigation speed
- recovery confidence

### Architect

Redesign:

- failure domains
- shared dependencies
- isolation
- graceful degradation
- failover assumptions
- recovery objectives
- test strategy

## Success Standard

A strong answer should explicitly reject:

- complete outage = only failure
- retries are always beneficial
- replicas = resilience
- failover = guaranteed recovery
- successful backup = proven recovery
- green health check = proven system health
- chaos = random destruction
