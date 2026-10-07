---
id: OBS-D00-021
domain: D00
topics:
  - D00-T017
level: L1-L2
type: observation
status: draft
estimated_time: 45-60m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# OBS-D00-021 — System Boundary, Flows, Constraints, and Bottlenecks

## Objective

Practice defining a useful system boundary, mapping end-to-end flows, identifying constraints, and locating the current bottleneck without reducing the problem to one component.

## Why This Matters

A system can look healthy component by component while the user-facing outcome is poor.

Systems thinking begins by asking:

> What is the complete system we need to understand for this outcome?

## Safety

This is a local reasoning exercise only.

Do not run load tests, stress systems, modify production capacity, or perform disruptive experiments.

## Scenario

Use this user journey:

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

The user goal is:

~~~text
Complete checkout successfully within the expected time.
~~~

## 1. Define the Narrow Boundary

Start with:

~~~text
Order Service Only
~~~

List what this boundary can explain.

Then list what it cannot explain.

## 2. Define the Wider Boundary

Expand to:

~~~text
Customer
→ Network Edge
→ Services
→ Database
→ External Payment
→ Queue
→ Worker
→ Operations
~~~

Explain why the wider boundary may be necessary for end-to-end checkout latency.

## 3. Map Inputs and Outputs

Identify system inputs such as:

- user requests
- inventory state
- payment availability
- configuration
- deployment version
- operator changes

Identify outputs such as:

- successful orders
- failed orders
- queue backlog
- latency
- retry volume
- support incidents

## 4. Map Flows

For the same system, map:

- request flow
- data flow
- payment flow
- message flow
- deployment/change flow
- alert/incident feedback flow

Explain why one architecture diagram can hide several different kinds of flow.

## 5. Identify State / Stocks

Identify accumulations such as:

- queue backlog
- active database connections
- pending orders
- retry backlog
- open incidents

Explain how accumulated state makes system behavior depend on history.

## 6. Identify Constraints

Review possible constraints:

- database connection pool
- payment-provider quota
- worker throughput
- queue-consumer capacity
- API CPU
- operator response capacity

Classify each as:

~~~text
Likely Constraint
Possible Constraint
Not Currently Limiting
Needs Evidence
~~~

## 7. Locate the Current Bottleneck

Use this evidence:

~~~text
API CPU = 45%
Database connections = 95% utilized
Payment latency = normal
Queue age = rising slowly
Worker CPU = 35%
Checkout latency = high
~~~

Identify the most likely active bottleneck.

Explain what evidence would confirm or reject it.

## 8. Bottleneck Migration

Assume database capacity is doubled.

Predict:

- what metric should improve
- what dependency may become the next bottleneck
- what should be re-measured

Explain why fixing one bottleneck changes the system.

## 9. Local vs Global Optimization

Review this proposal:

~~~text
"Make the API twice as fast."
~~~

Ask:

- will that increase useful checkout throughput?
- could it send more load to the database?
- could queue growth increase?
- could downstream failure worsen?

Explain why component speed is not the same as global performance.

## 10. Critical Path

Identify the likely critical path for checkout completion.

Mark which steps are:

- sequential
- parallel
- asynchronous
- user-blocking
- background

Explain why speeding a non-critical background step may not improve checkout latency.

## 11. Senior Engineer Connection

Use:

~~~text
Boundary
→ Flow
→ State
→ Constraint
→ Bottleneck
→ Critical Path
→ Global Outcome
~~~

## 12. SRE Connection

Connect this exercise to:

- SLOs
- saturation
- queue age
- dependency latency
- capacity planning
- incident scoping

## 13. Architect Connection

Ask:

- is the chosen boundary too narrow?
- which constraints are structural?
- where is coupling too tight?
- which system outcome matters most?
- what bottleneck is likely to appear next?

## Validation Checklist

- [ ] Defined narrow and wide system boundaries
- [ ] Mapped inputs and outputs
- [ ] Mapped multiple system flows
- [ ] Identified accumulated state / stocks
- [ ] Identified constraints
- [ ] Located a likely bottleneck
- [ ] Predicted bottleneck migration
- [ ] Compared local and global optimization
- [ ] Identified the critical path
- [ ] Connected the system map to SLO thinking

## Teach-Back

Explain:

> "A system boundary should be wide enough to include the interactions that determine the outcome, and a bottleneck is a property of the whole flow, not just one component."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
