# D00-T014 — Applied Observability Scenario

## Scenario

A checkout service uses:

~~~text
Client
→ API
→ Authentication
→ Order Service
→ Payment Provider
→ Database
→ Queue
→ Fulfillment Worker
~~~

Current observability design:

~~~text
- dashboard shows CPU, memory, disk, and node count
- logs are mostly free-form text
- request IDs exist only in the API
- trace context is not propagated to Payment or Queue
- deployment markers are not shown on dashboards
- request latency is tracked only as an average
- metrics include user_id and request_id labels
- all debug logs are retained for 180 days
- every trace is retained
- queue depth is monitored, but oldest-message age is not
- alerting pages on CPU > 80%
~~~

At 14:00:

~~~text
checkout p95 latency begins rising
payment latency rises at 14:03
retry volume rises at 14:05
queue age begins rising at 14:07
checkout errors rise at 14:08
Order Service v42 deploys at 14:10
CPU remains normal
Region B is much worse than Regions A and C
~~~

## Task 1 — Define the User-Centered Question

Define what the team should investigate first from the user’s perspective.

Include:

- affected journey
- symptom
- scope
- start time
- SLI impact

## Task 2 — Monitoring vs Observability

Explain which current checks are monitoring and which missing capabilities are observability gaps.

Explain why the team needs both.

## Task 3 — Metrics / Logs / Traces / Events

For the incident, identify what each signal type should contribute.

Use:

~~~text
Metrics
Logs
Traces
Events
~~~

## Task 4 — Correlation Identity

Design how:

- request ID
- trace ID
- correlation/workflow ID

should be propagated across:

~~~text
API
→ Order
→ Payment
→ Queue
→ Fulfillment
~~~

Explain why these identifiers should not be treated as universal synonyms.

## Task 5 — Structured Logging

Replace free-form logging with a structured schema.

Include fields for:

- timestamp
- service
- region
- version
- request/trace identity
- operation
- status
- duration
- dependency
- error type

Explain what should not be logged.

## Task 6 — Cardinality Review

Review these metric labels:

~~~text
service
region
endpoint
status
version
user_id
request_id
email
random_uuid
~~~

Classify which are useful and which are dangerous at metric scale.

Explain where high-cardinality context belongs instead.

## Task 7 — Latency Review

Explain why average latency is weak for this incident.

Propose a better view using:

- p50
- p95
- p99
- distribution/histogram thinking

Do not perform backend-specific histogram math.

## Task 8 — Regional Segmentation

Explain why comparing:

~~~text
Region A
Region B
Region C
~~~

is useful.

Describe how broad aggregation could hide the problem.

## Task 9 — Queue Observability

Current dashboard shows queue depth only.

Add:

- oldest-message age
- producer rate
- consumer rate
- retry volume
- dead-letter volume

Explain why queue age can be critical.

## Task 10 — Change Markers

The Order Service v42 deployment happens after latency had already started increasing.

Explain:

- why the deployment is still relevant evidence
- why it does not automatically prove causation
- what additional evidence is needed

## Task 11 — Ranked Hypotheses

Create at least four ranked hypotheses, such as:

- payment dependency slowdown
- retry amplification
- regional network issue
- Order Service regression
- queue-consumer slowdown

For each use:

~~~text
Supporting Evidence
Missing Evidence
Contradicting Evidence
Next Safe Check
~~~

## Task 12 — Sampling and Retention

The team keeps every trace and 180 days of debug logs.

Redesign conceptually:

- which signals deserve full retention
- which can be sampled
- which need shorter retention
- which are security/privacy sensitive

Explain the trade-off.

## Task 13 — Dashboard Redesign

Replace:

~~~text
CPU
Memory
Disk
Node Count
~~~

with a hierarchy:

~~~text
User Impact
→ Service Behavior
→ Dependencies
→ Queues
→ Resources
→ Changes
→ Diagnostics
~~~

Include key panels.

## Task 14 — Alert Redesign

Replace:

~~~text
CPU > 80%
→ Page
~~~

with a stronger user-impact-aware alert.

Include:

- checkout symptom
- region
- dependency context
- version
- start time
- dashboard/runbook reference

## Task 15 — Recovery Validation

Assume Payment latency returns to normal.

Define what evidence proves the service is actually recovered.

Include:

- checkout success
- p95 latency
- retry rate
- queue age
- regional health
- end-to-end user journey

## Task 16 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Impact
→ Scope
→ Timeline
→ Changes
→ Service Signals
→ Dependencies
→ Resources
→ Logs / Traces
→ Hypothesis
→ Safe Validation
~~~

### SRE

Connect:

- SLI/SLO
- alert quality
- missing telemetry
- MTTR
- error-budget impact
- recovery validation

### Architect

Redesign:

- telemetry standards
- context propagation
- cardinality rules
- sampling/retention policy
- dashboard hierarchy
- production-readiness observability gate

## Success Standard

A strong answer should explicitly reject:

- observability = dashboard count
- telemetry = observability
- CPU threshold = sufficient service alert
- user_id/request_id as safe metric labels by default
- average latency = sufficient latency analysis
- deployment marker = proof of causation
- queue depth = complete queue health
- collecting all telemetry forever = mature design
