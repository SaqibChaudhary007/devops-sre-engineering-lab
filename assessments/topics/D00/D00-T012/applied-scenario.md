# D00-T012 — Applied Reliability Scenario

## Scenario

A customer-facing checkout platform uses:

~~~text
Client
→ DNS
→ Load Balancer
→ API
→ Authentication
→ Order Service
→ Database
→ Payment Provider
→ Queue
→ Fulfillment Worker
~~~

Current design:

~~~text
- 3 API replicas
- all 3 replicas run in one availability zone
- database primary and standby use the same storage failure domain
- normal traffic consumes 75% of safe application capacity
- checkout fails if the recommendation service is unavailable
- database backups run every 15 minutes
- restores have never been tested
- RTO is documented as 30 minutes
- RPO is documented as 15 minutes
- alerting is mostly CPU and memory thresholds
- deployment rollback exists, but schema changes are not always backward-compatible
- runbook exists but has not been exercised
- on-call ownership is unclear
~~~

At 10:00:

~~~text
One application node fails
→ capacity drops
→ remaining replicas approach saturation
→ latency rises
→ retries increase
→ checkout errors rise
→ CPU alert fires at 10:08
→ team starts mitigation at 10:16
→ recommendation service also begins failing
→ checkout remains fully blocked
→ service returns to acceptable state at 10:38
~~~

## Task 1 — Define the Critical User Journey

Define what "successful checkout" means from the user's perspective.

Include:

- correctness
- success
- latency
- payment state
- order state
- fulfillment acceptance

## Task 2 — Reliability vs Availability

Explain whether each condition is:

- available
- reliable
- durable
- resilient
- recoverable

for the incident.

Explain why "API processes are running" is weak reliability evidence.

## Task 3 — Failure Domains

Identify shared failure domains in:

- application replicas
- database primary/standby
- recommendation dependency
- payment dependency

Explain where redundancy is correlated.

## Task 4 — Blast Radius

Estimate the blast radius of:

- one API process crash
- one zone failure
- database storage failure
- payment provider outage
- recommendation outage

## Task 5 — Graceful Degradation

Redesign recommendation behavior:

~~~text
Recommendation unavailable
→ Checkout continues
→ Recommendation UI hidden
~~~

Explain why this improves reliability only if recommendations are noncritical to correctness.

## Task 6 — Capacity Headroom

Normal traffic uses 75% of safe capacity.

Explain what happens after losing significant capacity.

Discuss:

- failover headroom
- retry load
- latency
- saturation
- maintenance margin

## Task 7 — Incident Timeline

Using the given timestamps, identify:

- time to detect
- time to respond
- time to recover

Explain why each should be measured separately.

## Task 8 — Alert Quality

Current alert:

~~~text
CPU > threshold
~~~

Design a stronger alert approach using:

- checkout success ratio
- latency
- saturation
- retry rate
- queue age
- dependency failures

## Task 9 — SLI, SLO, SLA

Propose:

- one checkout SLI
- one checkout SLO
- one example external SLA statement at a conceptual level

Explain why they differ.

## Task 10 — Error Budget

Assume:

~~~text
Checkout SLO = 99.9%
~~~

Explain:

- what the error budget represents
- what consuming too much of it should influence
- why it should not be treated as a vanity metric

## Task 11 — Backup and Recovery

Backups run every 15 minutes but restores have never been tested.

Explain what is known and unknown.

List what a recovery test should prove:

- restore success
- data correctness
- recovery timing
- access/permissions
- application validation

## Task 12 — RTO / RPO

Explain:

~~~text
RTO = 30 min
RPO = 15 min
~~~

Then decide whether the incident met the RTO.

Explain why backup frequency alone does not prove the RPO.

## Task 13 — Rollback vs Roll-Forward

A deployment caused the incident, but the new database schema is not backward-compatible.

Explain why rollback may be unsafe.

Compare rollback and roll-forward.

## Task 14 — Runbook and Ownership

Design a minimal incident runbook:

~~~text
Trigger
Impact
Evidence
Decision Point
Mitigation
Recovery
Validation
Escalation
~~~

Explain why unclear ownership increases recovery time.

## Task 15 — Production Readiness

Score:

~~~text
Ready
Partially Ready
Not Ready
~~~

for:

- critical-user-journey SLI
- SLO
- capacity headroom
- failure-domain independence
- graceful degradation
- backup restore testing
- failover validation
- dashboards
- actionable alerts
- rollback/roll-forward plan
- runbook
- on-call ownership

## Task 16 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Impact
→ Critical Journey
→ Failure Domain
→ Capacity
→ Dependencies
→ Evidence
→ Safe Mitigation
→ Recovery
→ Validation
~~~

### SRE

Connect the incident to:

- SLI/SLO
- error budget
- time to detect
- time to respond
- time to recover
- saturation
- retry pressure
- alert quality

### Architect

Redesign:

- failure-domain placement
- headroom
- degradation boundaries
- recovery objectives
- tested backup/restore
- change safety
- operational ownership

## Success Standard

A strong answer should explicitly reject:

- reliability = 100% uptime
- replicas = automatic resilience
- backup = proven recovery
- failover = guaranteed recovery
- CPU threshold = sufficient reliability monitoring
- RTO = RPO
