# D00-T017 — Teach-Back Assessment

## Goal

Demonstrate that you can explain how interactions, feedback, constraints, delays, and dependencies create whole-system behavior.

## Task A — Beginner

Explain:

- system
- boundary
- component
- relationship
- flow

## Task B — Stocks and Flows

Explain:

~~~text
Inflow
→ Stock / Accumulation
→ Outflow
~~~

Use queue backlog as the example.

## Task C — Bottlenecks

Explain why fixing one bottleneck can expose another.

Then explain why every component should not be optimized independently.

## Task D — Feedback Loops

Teach:

~~~text
Reinforcing Loop
vs
Balancing Loop
~~~

Use retries and autoscaling as examples.

## Task E — Delays and Oscillation

Explain how delayed feedback can make a corrective action overshoot or oscillate.

## Task F — Coupling and Common-Mode Failure

Explain:

- tight coupling
- hidden coupling
- shared dependency
- common-mode failure

Then explain why redundancy is not the same as independence.

## Task G — Cascading Failure

Teach:

~~~text
Dependency Slowdown
→ Retries
→ Load
→ Saturation
→ Queue Growth
→ Alert Storm
→ Human Overload
~~~

## Task H — Backpressure

Explain why backpressure must propagate across the whole upstream/downstream chain.

## Task I — Second-Order Effects

Explain why a successful first-order intervention can create a new bottleneck or side effect elsewhere.

## Task J — Architect

Explain how you would use:

- system boundary
- feedback loops
- bottlenecks
- leverage points
- SLOs
- second-order effects

to review a production architecture.

## Scoring

Score 1–5 for:

- correctness
- clarity
- boundary/flow reasoning
- bottleneck/global-optimization reasoning
- feedback/delay reasoning
- failure-propagation reasoning
- SRE/system-outcome reasoning
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.
