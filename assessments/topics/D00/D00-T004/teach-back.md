# D00-T004 — Teach-Back Assessment

## Goal

Demonstrate that you can explain architecture at different levels without hiding behind tool names.

## Task A — Beginner

Explain:

- client
- server
- frontend
- backend
- database

Use one simple web-shopping example.

## Task B — Engineer

Explain this architecture:

~~~text
User
→ Load Balancer
→ App Instances
→ Database
→ External API
~~~

For each component, explain its responsibility.

## Task C — Senior Engineer

Explain why this statement is wrong:

> "We added more app servers, so the system should be faster."

Include:

- bottlenecks
- state
- database
- dependencies
- queues/waiting

## Task D — SRE

Explain how one slow dependency can create an SLO problem for an otherwise healthy upstream service.

Include:

- latency propagation
- saturation
- retries
- user impact
- telemetry

## Task E — Architect

Compare:

~~~text
Monolith
vs
Modular Monolith
vs
Microservices
~~~

Discuss:

- deployment
- team ownership
- scaling
- failure isolation
- data
- observability
- security
- cost
- operational maturity

## Diagram Challenge

Draw from memory:

~~~text
User
↓
Entry Point
↓
Application
↓
Data Store
↓
External Dependency
~~~

Then add:

- one cache
- one queue
- one single point of failure
- one stateful component
- one failure propagation path

## Scoring

Score 1–5 for:

- correctness
- clarity
- architecture reasoning
- failure reasoning
- scaling reasoning
- SRE connection
- trade-off awareness

Target: average 4/5 with no critical misconception.
