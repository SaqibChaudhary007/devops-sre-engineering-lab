# D00-T004 — Applied Architecture Scenario

## Scenario

Architecture:

~~~text
Users
  ↓
Load Balancer
  ↓
┌───────────────┬───────────────┐
│ App Instance A│ App Instance B│
└───────────────┴───────────────┘
          ↓
       Database
          ↓
  External Payment API
~~~

Observed behavior:

~~~text
Traffic:                 increased 2x
App CPU:                 35–45%
App memory:              normal
App instance count:      increased from 2 to 6
User latency:            still high
Database latency:        elevated
Payment API latency:     sometimes very high
Error rate:              moderate
Session behavior:        some users lose cart/session state after scaling
Recent change:           app tier scaled horizontally
~~~

## Task 1 — Impact and Scope

Answer:

1. What is the user-visible impact?
2. Which symptoms point to more than one problem?
3. What information is still missing before declaring root cause?

## Task 2 — Architecture Map

Draw the request path and mark:

- traffic entry point
- application tier
- stateful dependencies
- external dependency
- likely latency accumulation points
- possible single points of failure

## Task 3 — Why Scaling Did Not Fix It

Explain why increasing app instances from 2 to 6 may not reduce latency.

Consider:

- database latency
- external payment latency
- connection pools
- state
- shared dependencies
- moved bottleneck

## Task 4 — Session/State Problem

Users sometimes lose cart/session state after adding more instances.

What hypothesis does this suggest?

Explain:

- why local in-memory state can cause inconsistent behavior
- what sticky sessions might change
- why externalized session state may improve replaceability
- what new dependency externalized state creates

## Task 5 — Dependency Latency

Payment API latency is sometimes very high.

Explain how this can affect:

~~~text
Payment API
→ App waiting
→ Worker/concurrency pressure
→ User latency
~~~

What evidence would you collect to confirm this path?

## Task 6 — Senior Engineer Response

Write an investigation sequence using:

~~~text
Impact
→ Request Path
→ State Location
→ Dependency Latency
→ Database Behavior
→ Evidence
→ Hypotheses
→ Safe Mitigation
→ Root Cause
→ Prevention
~~~

## Task 7 — SRE View

Answer:

1. Which user-facing SLIs would matter most?
2. What dependency signals would you want?
3. What would indicate saturation rather than simple utilization?
4. Which failures could degrade gracefully?
5. Which conditions should page on-call?

## Task 8 — Architect View

The business expects traffic to grow 10x in one year.

Evaluate architecture questions around:

- monolith vs service decomposition
- stateless app instances
- database capacity
- caching
- synchronous payment dependency
- asynchronous workflows
- failure isolation
- observability
- cost
- team operational maturity

Do not answer with "use microservices" unless requirements justify it.

## Success Standard

A strong answer identifies multiple independent constraints: state placement, database latency and external dependency latency. It explains why scaling only the app tier may not help, and recommends architecture decisions based on evidence and requirements rather than trend-driven choices.
