---
id: EXP-D00-011
domain: D00
topics:
  - D00-T008
level: L2-L3
type: experiment
status: draft
estimated_time: 50-70m
environment:
  - Local workstation
  - Text editor or diagram tool
evidence_status:
  - DRAFT
---

# EXP-D00-011 — Dependency Graph, State Boundary, and Concurrency Design

## Objective

Reason about infrastructure dependencies, state/ownership boundaries, and concurrent changes without using a real IaC tool or cloud account.

## Safety

This is a local architecture exercise only.

No infrastructure is created, updated, or destroyed.

## Scenario

A company runs three services:

~~~text
Shared Network
├── payments-api
├── orders-api
└── notifications-api
~~~

Each service has:

- application compute
- database
- service identity
- monitoring configuration

The shared network has:

- virtual network
- subnets
- routing
- shared load-balancing layer

Two teams work independently:

~~~text
Platform Team
Product Teams
~~~

## 1. Build the Dependency Graph

Draw a graph showing:

~~~text
Network
→ Subnet
→ Load Balancer
→ Application
→ Database
~~~

Then add:

- service identity
- monitoring
- outputs consumed by downstream components

Mark dependencies as:

~~~text
Implicit
Explicit
Operational
~~~

## 2. Ordering Reasoning

For each relationship, answer:

- what must exist first?
- what can be created in parallel?
- what failure would occur if ordering is wrong?
- which dependency should be inferred from a reference?
- which dependency may need explicit coordination?

## 3. Design State / Ownership Boundaries

Compare three options.

### Option A — One Global State

~~~text
network
payments
orders
notifications
all in one state
~~~

### Option B — One State per Environment

~~~text
production state
staging state
development state
~~~

### Option C — Platform + Service States

~~~text
platform-network state
payments state
orders state
notifications state
~~~

For each option, score:

- blast radius
- team autonomy
- coordination overhead
- dependency complexity
- recovery complexity
- access-control clarity

Use:

~~~text
Low
Medium
High
~~~

## 4. Choose a Boundary

Pick one design and explain:

- why it matches ownership
- what dependencies cross state boundaries
- which outputs/inputs must be shared
- who is allowed to apply each state
- what happens during an incident

Do not claim one model is always correct.

## 5. Concurrency Scenario

Assume:

~~~text
Engineer A
→ changes network route

Engineer B
→ scales payments compute

Both apply at the same time.
~~~

Answer:

- if they share one state, what conflict can occur?
- how can state locking help?
- what does locking not solve?
- if they use separate states, what dependency risk remains?

## 6. Backend Capability Nuance

Explain why this statement is unsafe:

> "Remote state automatically means safe locking."

Use the verified rule:

> Locking depends on the selected tool/backend capabilities.

## 7. Shared Output Scenario

The payments service needs the shared subnet ID.

Model:

~~~text
Platform State
→ subnet_id output
→ Payments State input
~~~

Discuss:

- coupling
- version/change coordination
- stale values
- ownership
- access control

## 8. State Security

List what a state system may expose:

- resource IDs
- topology
- metadata
- configuration
- possibly sensitive material depending on tool/provider

Then define minimum controls:

- least privilege
- encryption
- backup
- auditability
- controlled access

## 9. Senior Engineer Connection

A senior engineer should ask:

~~~text
Who owns this state?
What changes together?
What should fail together?
What should not fail together?
Where can concurrent changes collide?
~~~

## 10. SRE Connection

Connect state boundaries to:

- incident blast radius
- recovery speed
- emergency change
- audit history
- dependency visibility

## 11. Architect Connection

Explain how organizational boundaries can become IaC architecture boundaries.

Discuss when:

- one shared platform state is reasonable
- service-level states are safer
- too many states create coordination cost

## Validation Checklist

- [ ] Built the dependency graph
- [ ] Classified dependency types
- [ ] Compared three state-boundary models
- [ ] Selected and defended one design
- [ ] Analyzed a concurrency scenario
- [ ] Explained locking limitations
- [ ] Modeled cross-state outputs
- [ ] Defined state-security controls

## Teach-Back

Explain:

> "State boundaries are not just file organization; they define ownership, coordination, and blast radius."

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after completion and review.
