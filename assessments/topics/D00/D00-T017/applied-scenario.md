# D00-T017 — Applied Systems Thinking Scenario

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

The platform also shares:

~~~text
- one DNS path
- one database cluster
- one deployment pipeline
- one cloud IAM quota
- one on-call team
~~~

Observed behavior:

~~~text
- checkout p95 latency rises
- API CPU remains moderate
- database connection pool is near saturation
- payment latency rises slightly
- clients retry on timeout
- retry volume increases
- queue depth looks stable
- oldest-message age rises
- autoscaler adds API replicas after a delay
- database pressure increases further
- alert volume rises
- on-call response slows
~~~

## Task 1 — Define the System Boundary

Create:

- a narrow boundary
- a wider boundary

Explain which is more useful for checkout SLO analysis and why.

## Task 2 — Map Inputs, Outputs, and Flows

Identify:

- request flow
- data flow
- payment flow
- queue/message flow
- deployment/change flow
- alert/human feedback flow

## Task 3 — Identify Stocks and State

Identify accumulations such as:

- queue backlog
- active connections
- retry backlog
- pending work
- open alerts/incidents

Explain why history matters.

## Task 4 — Locate the Bottleneck

Use the evidence to identify the most likely active constraint.

Explain what evidence would confirm or reject it.

## Task 5 — Bottleneck Migration

Assume database capacity is increased.

Predict:

- what improves first
- what constraint may appear next
- what must be re-measured

## Task 6 — Local vs Global Optimization

Evaluate:

~~~text
"Increase API replicas by 5x."
~~~

Explain:

- when it helps
- when it does nothing
- when it worsens downstream pressure

## Task 7 — Reinforcing Feedback Loop

Model:

~~~text
Latency ↑
→ Timeouts ↑
→ Retries ↑
→ Load ↑
→ Latency ↑
~~~

Explain why this loop can amplify failure.

## Task 8 — Balancing Feedback Loop

Model autoscaling:

~~~text
Load ↑
→ Capacity Added
→ Load per Instance ↓
~~~

Then add delays and explain why the balancing loop may overshoot.

## Task 9 — Queue Analysis

Given:

~~~text
Queue depth = stable
Oldest message age = rising
Consumer throughput = falling
~~~

Explain why the queue is unhealthy despite stable depth.

## Task 10 — Backpressure

Redesign the overloaded path conceptually:

~~~text
Downstream Saturated
→ Signal / Reject / Slow Admission
→ Upstream Reduces Work
→ Dependency Recovers
~~~

Explain why upstream retry behavior must respect the signal.

## Task 11 — Hidden Coupling

Identify how these shared resources create common-mode risk:

- DNS
- database
- IAM quota
- deployment pipeline
- on-call team

## Task 12 — Cascading Failure

Map:

~~~text
Payment Slowdown
→ Checkout Latency
→ Retries
→ DB Connection Growth
→ Queue Delay
→ Alert Storm
→ On-Call Overload
~~~

Identify:

- initiating condition
- propagation path
- reinforcing loops
- human-system interaction
- user impact

## Task 13 — Redundancy vs Independence

Review:

~~~text
"We have two replicas, so we are resilient."
~~~

Check shared:

- database
- region
- credentials
- control plane
- deployment pipeline

Explain why redundancy is not the same as independence.

## Task 14 — Second-Order Effects

Intervention:

~~~text
Add Cache
~~~

First-order effect:

~~~text
Database load ↓
~~~

Now identify possible second-order effects.

## Task 15 — Leverage Points

Rank these interventions:

- add more API CPU
- increase retry count
- reduce duplicate work
- improve backpressure
- isolate shared database pressure
- change timeout policy
- improve queue admission

Explain assumptions.

## Task 16 — Event → Pattern → Structure → Policy

Use:

~~~text
Event:
Checkout outage

Pattern:
Occurs during downstream slowdown

Structure:
Retries + shared database + delayed autoscaling + weak backpressure

Policy / Mental Model:
"Retry more to improve reliability"
~~~

Explain why the structural/policy level may contain the highest-leverage fix.

## Task 17 — Senior / SRE / Architect Response

### Senior Engineer

Use:

~~~text
Boundary
→ Flow
→ State
→ Constraint
→ Feedback
→ Delay
→ Hypothesis
→ Intervention
~~~

### SRE

Connect:

- SLO impact
- retry amplification
- queue health
- saturation
- overload protection
- alert feedback
- recovery stability

### Architect

Redesign:

- shared dependencies
- failure domains
- backpressure
- retry ownership
- autoscaling signals
- intervention boundaries
- blast radius

## Success Standard

A strong answer should explicitly reject:

- healthy components = healthy system
- more API capacity = universal fix
- retries = purely local behavior
- autoscaling = instant capacity
- stable queue depth = healthy queue
- redundancy = independence
- every incident = one isolated root cause
