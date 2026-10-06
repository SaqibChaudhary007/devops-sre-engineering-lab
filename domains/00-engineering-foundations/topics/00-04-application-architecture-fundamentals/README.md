---
id: D00-T004
domain: D00
title: Application Architecture Fundamentals
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
estimated_time:
  theory: 5-7h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
    - D00-T003
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Follow the Request
  - Five Levels
  - Architecture With Saqib
---

# 00.04 — Application Architecture Fundamentals

## Start Here

So far, you have learned:

~~~text
00.01 — Computer resources
00.02 — Operating system
00.03 — Software lifecycle
~~~

Now we connect individual applications into systems.

The key question is:

> How do application components communicate, where does state live, and how does a user request move through the system?

This topic builds the architecture mental model you will need before cloud, Kubernetes, distributed systems, observability, SRE and system design.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- client and server
- request and response
- frontend and backend
- three-tier architecture
- monolith
- modular monolith
- microservices
- API
- synchronous vs asynchronous communication
- stateless vs stateful application behavior
- database/data-store role
- cache
- load balancer
- queue/broker at a high level
- dependency
- service boundary
- horizontal scaling implications
- availability implications
- why architecture creates operational trade-offs
- how to follow one user request through multiple components
- why "microservices" is not automatically better

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)

You should already understand:

- process
- runtime
- artifact
- configuration
- network at a high level
- storage/persistence
- dependency
- startup/runtime failure
- application version identity

---

# 3. The First Architecture Mental Model

A very simple application might look like:

~~~text
User
 ↓
Application
 ↓
Data
~~~

A more realistic web application often looks like:

~~~text
User
  ↓
Client / Browser
  ↓
Load Balancer / Entry Point
  ↓
Application
  ↓
Database
~~~

As systems grow, more components may appear:

~~~text
Users
  ↓
Frontend
  ↓
API / Backend
  ↓
Database
  ↓
Cache
  ↓
Message Queue
  ↓
External Services
~~~

Architecture is the arrangement of components, responsibilities, communication paths and data/state.

---

# 4. Client and Server

A **client** requests a service.

A **server** provides a service.

Example:

~~~text
Browser
  ↓ request
Web Server
  ↓ response
Browser
~~~

The client/server model appears everywhere:

- browser → website
- mobile app → API
- application → database
- service → service
- monitoring agent → monitoring backend

## Key Lesson

Client and server describe roles in an interaction.

One system can be a server in one interaction and a client in another.

Example:

~~~text
Mobile App
   ↓
Backend API
   ↓
Database
~~~

The backend is:

- server to the mobile app
- client to the database

---

# 5. Request and Response

A request/response interaction is a common communication model.

~~~text
Client
  ↓ Request
Server
  ↓ Processing
Server
  ↓ Response
Client
~~~

A request may include:

- operation/method
- path/resource
- headers/metadata
- body/payload
- authentication information

A response may include:

- status
- headers/metadata
- body/data
- error information

Deep HTTP belongs to D02 Networking and later API/system-design topics.

---

# 6. Frontend and Backend

## Frontend

The user-facing part of an application.

Examples:

- browser UI
- mobile app UI
- desktop UI

## Backend

The server-side logic that processes requests and interacts with data/dependencies.

A simple model:

~~~text
User
 ↓
Frontend
 ↓
Backend
 ↓
Database
~~~

The frontend and backend may be:

- part of one deployable application
- separate applications
- hosted independently
- scaled independently

Architecture determines these boundaries.

---

# 7. Three-Tier Architecture

A classic mental model:

~~~text
Presentation Tier
      ↓
Application / Logic Tier
      ↓
Data Tier
~~~

Example:

~~~text
Browser
  ↓
Web / API Application
  ↓
Database
~~~

## Why Tiers Exist

Separating responsibilities can improve:

- maintainability
- scaling choices
- security boundaries
- team ownership
- troubleshooting clarity

But more layers also create:

- more dependencies
- more network paths
- more failure points
- more operational complexity

---

# 8. Monolith

A monolith is an application where many business capabilities are delivered as one main deployable unit.

Simplified:

~~~text
             Monolithic Application
┌───────────────────────────────────────┐
│ Authentication                        │
│ Orders                                │
│ Payments                              │
│ Inventory                             │
│ Notifications                         │
└───────────────────────────────────────┘
                  ↓
               Database
~~~

## Advantages

A monolith can offer:

- simple deployment model
- simpler local development
- fewer network calls between internal modules
- easier transaction boundaries
- lower operational overhead

## Challenges

As it grows:

- deployments can affect many features
- scaling one function may require scaling whole app
- codebase can become tightly coupled
- ownership can become difficult

---

# 9. Modular Monolith

A modular monolith remains one deployable application but has stronger internal boundaries.

~~~text
One Deployable Application

┌───────────────────────────┐
│ Auth Module               │
├───────────────────────────┤
│ Order Module              │
├───────────────────────────┤
│ Inventory Module          │
├───────────────────────────┤
│ Payment Module            │
└───────────────────────────┘
~~~

This can provide:

- simpler operations than microservices
- clearer internal ownership
- better separation of concerns

Important lesson:

> Monolith does not automatically mean badly designed.

---

# 10. Microservices

Microservices split capabilities into independently deployable services.

~~~text
Client
  ↓
API Gateway / Entry
  ↓
┌──────────┬──────────┬───────────┐
│ Auth     │ Orders   │ Inventory │
└──────────┴──────────┴───────────┘
     ↓          ↓           ↓
   Data       Data        Data
~~~

Potential benefits:

- independent deployment
- independent scaling
- clearer service ownership
- technology flexibility
- smaller deployment boundaries

But microservices introduce major costs:

- network failures
- distributed tracing needs
- service discovery
- version compatibility
- data consistency challenges
- more deployments
- more observability
- more security boundaries
- more operational burden

---

# 11. Monolith vs Microservices

Do not ask:

> Which architecture is better?

Ask:

> Which architecture fits the requirements, team, scale and operational capability?

A simplified comparison:

| Dimension | Monolith | Microservices |
|---|---|---|
| Deployment | one/few units | many independent units |
| Network calls | fewer internal | many inter-service |
| Operational complexity | lower | higher |
| Independent scaling | limited/coarse | finer-grained |
| Failure isolation | can be broad | potentially narrower, but distributed |
| Data consistency | simpler | often harder |
| Team autonomy | can be lower | can be higher |
| Observability need | moderate | much higher |

---

# 12. API

An API is an interface through which software components interact.

Conceptually:

~~~text
Client
  ↓
API Contract
  ↓
Service
~~~

An API contract defines expectations such as:

- operation
- request format
- response format
- status/error behavior
- authentication
- versioning

An API is not just a URL.

It is a contract between systems.

---

# 13. API Contract

Suppose:

~~~text
GET /orders/123
~~~

The important part is not only the endpoint.

The contract includes:

~~~text
Request expectations
Response schema
Status behavior
Authentication
Error semantics
Version compatibility
~~~

Why this matters operationally:

> A backend change can break clients even when both services are "up."

Availability is not only process uptime.

Compatibility matters too.

---

# 14. Synchronous Communication

Synchronous communication means the caller waits for a response.

~~~text
Service A
   ↓ request
Service B
   ↓ processing
Service B
   ↓ response
Service A continues
~~~

Examples:

- HTTP API call
- synchronous database query
- RPC request

## Risk

If B is slow:

~~~text
B slow
  ↓
A waits
  ↓
A workers remain occupied
  ↓
queue grows
  ↓
A becomes slow
~~~

One slow dependency can propagate latency.

---

# 15. Asynchronous Communication

Asynchronous communication allows work to be accepted and processed later.

~~~text
Producer
   ↓
Queue / Broker
   ↓
Consumer
~~~

The producer may not wait for the final work result.

Potential advantages:

- decoupling
- buffering
- workload smoothing
- resilience to temporary consumer slowdown

Challenges:

- eventual processing
- duplicate delivery handling
- ordering
- retries
- backlog growth
- harder end-to-end tracing

Deep messaging belongs to D26.

---

# 16. Stateless Application

A stateless application does not depend on unique local in-memory/session state across requests in a way that forces the same user to reach the same instance.

Conceptually:

~~~text
Request 1 → Instance A
Request 2 → Instance B
Request 3 → Instance C
~~~

If all instances can handle any request, horizontal scaling is usually easier.

Examples of state may be stored externally:

- database
- distributed cache
- object storage

---

# 17. Stateful Application

A stateful application maintains important state that affects future processing.

State can include:

- sessions
- files
- database records
- local queues
- in-memory workflow state

Example:

~~~text
User Session
   ↓
Instance A local memory
~~~

If the next request reaches Instance B:

~~~text
Instance B
   ↓
Session not present
~~~

This can create scaling and failover complexity.

---

# 18. State vs Stateless Is Not Binary

A service may be mostly stateless but still depend on external state.

Example:

~~~text
Stateless API Instances
      ↓
Shared Database
~~~

The application instances are replaceable.

The overall system is still stateful because the database holds persistent business state.

This distinction is extremely important.

---

# 19. Database / Data Store

A data store persists or manages application state.

Examples:

- relational database
- document database
- key-value store
- object storage
- time-series database

At D00 level, understand:

~~~text
Application
  ↓
Data Store
  ↓
Persistent State
~~~

Data stores introduce:

- availability concerns
- latency
- capacity
- consistency
- backup/recovery needs
- scaling considerations

Deep data-system design comes later.

---

# 20. Cache

A cache stores frequently/recently needed data closer to the application to reduce latency or repeated expensive work.

~~~text
Application
   ↓
Cache
  /   \
Hit   Miss
 |      |
Fast   Database
        ↓
      Result
~~~

Potential benefits:

- lower latency
- reduced backend load
- improved throughput

Potential problems:

- stale data
- invalidation
- cache stampede
- additional dependency
- memory pressure

A cache does not remove the source of truth.

---

# 21. Load Balancer

A load balancer distributes incoming traffic across multiple application instances.

~~~text
Users
  ↓
Load Balancer
  ↓
┌────────┬────────┬────────┐
│ App A  │ App B  │ App C  │
└────────┴────────┴────────┘
~~~

Potential benefits:

- horizontal scaling
- traffic distribution
- instance failure handling
- maintenance flexibility

But the load balancer itself becomes an important component and failure path.

---

# 22. Horizontal Scaling

Horizontal scaling adds more instances.

~~~text
1 App Instance
      ↓
3 App Instances
~~~

This is easiest when application instances are:

- stateless
- independently replaceable
- using shared/external state

But scaling the application does not automatically scale:

- database
- external API
- queue consumer capacity
- storage
- network

The bottleneck can move.

---

# 23. Vertical Scaling

Vertical scaling makes one instance larger.

Example:

~~~text
4 CPU / 8 GB
       ↓
16 CPU / 64 GB
~~~

Advantages:

- simple
- fewer distributed components

Limitations:

- finite machine size
- larger failure impact
- cost
- downtime/migration constraints

Architecture decisions often combine vertical and horizontal scaling.

---

# 24. Service Dependency

A dependency is any component another component requires.

Example:

~~~text
Checkout Service
  ├── Payment Service
  ├── Inventory Service
  ├── Database
  └── Email Service
~~~

The availability of checkout may depend on all or some of them.

This creates a major architecture lesson:

> Your service reliability can be limited by dependencies you do not own.

---

# 25. Dependency Chain

Consider:

~~~text
User
 ↓
Frontend
 ↓
API
 ↓
Order Service
 ↓
Payment Service
 ↓
Bank API
~~~

End-to-end latency includes multiple stages.

Failure can occur at any stage.

This is why distributed systems require:

- timeouts
- retries
- observability
- fallbacks
- careful dependency design

These topics are introduced later in D00 and deeply in distributed systems/SRE.

---

# 26. Tight Coupling

Components are tightly coupled when a change/failure in one strongly affects another.

Examples:

- hardcoded assumptions
- shared database tables across services
- synchronous dependency chains
- incompatible API changes

Tight coupling can increase:

- change risk
- coordination overhead
- failure propagation

---

# 27. Loose Coupling

Loosely coupled components interact through clearer boundaries/contracts.

Potential benefits:

- independent change
- easier ownership
- reduced coordination
- better failure isolation

But loose coupling does not mean:

> No dependency.

It means dependency is better bounded.

---

# 28. Service Boundary

A service boundary defines what responsibility belongs inside a component and what belongs outside.

Good boundaries often align with:

- business capability
- data ownership
- team ownership
- change patterns

Bad boundaries can create excessive communication.

Example:

~~~text
Order Service
→ Pricing Service
→ Tax Service
→ Discount Service
→ Customer Service
→ Inventory Service
~~~

A single user request can become a long dependency chain.

---

# 29. Shared Database Problem

Suppose many services directly modify the same database schema.

~~~text
Service A ─┐
Service B ─┼→ Shared Database
Service C ─┘
~~~

This can create:

- schema coupling
- deployment coordination
- ownership ambiguity
- failure blast radius

But separate databases per service also introduce:

- duplication
- consistency challenges
- reporting complexity
- operational cost

Again: trade-offs.

---

# 30. Request Path

A DevOps/SRE engineer should be able to draw the path of a user request.

Example:

~~~text
User
 ↓
DNS
 ↓
Load Balancer
 ↓
Frontend
 ↓
API
 ↓
Database
 ↓
External Payment API
~~~

For each hop, ask:

~~~text
What can fail?
What can be slow?
What evidence exists?
Who owns it?
What happens if unavailable?
~~~

This becomes the foundation for troubleshooting distributed applications.

---

# 31. Failure Propagation

Imagine:

~~~text
Database slows
    ↓
API requests wait
    ↓
Application worker pool fills
    ↓
Load balancer queues/receives slow responses
    ↓
Users see latency
~~~

The visible symptom is:

> Website slow.

The original problem might be the database.

This connects architecture directly to troubleshooting.

---

# 32. Cascading Failure — Preview

A small failure can trigger additional failures.

Example:

~~~text
Dependency slows
     ↓
Client retries aggressively
     ↓
More traffic reaches dependency
     ↓
Dependency becomes slower
     ↓
More retries
~~~

This is a retry storm.

Deep resilience patterns come later.

At this stage retain:

> Architecture controls how failure spreads.

---

# 33. Single Point of Failure

A single point of failure is a component whose failure can make the whole service unavailable.

Example:

~~~text
Users
 ↓
Single App Instance
 ↓
Database
~~~

If the only app instance fails:

~~~text
Service unavailable
~~~

Redundancy can reduce this risk, but it also increases complexity and cost.

---

# 34. High Availability — Introductory View

High availability aims to reduce service interruption through design.

Examples:

- multiple app instances
- replicated components
- load balancing
- failover
- health checks

But:

> Multiple instances alone do not guarantee high availability.

Shared dependencies and failure domains matter.

---

# 35. External Dependencies

Applications often depend on third-party systems.

Examples:

- payment provider
- SMS provider
- email service
- identity provider
- maps API

You may not control:

- uptime
- latency
- limits
- change schedule

Architecture must account for this.

---

# 36. API Gateway — Introductory View

An API gateway can provide a common entry point to multiple backend services.

~~~text
Clients
   ↓
API Gateway
   ↓
┌─────────┬──────────┬──────────┐
│ Orders  │ Users    │ Payments │
└─────────┴──────────┴──────────┘
~~~

Possible responsibilities:

- routing
- authentication
- rate limiting
- request transformation
- observability

But it can also become:

- central complexity
- bottleneck
- important failure point

---

# 37. Architecture Is About Trade-Offs

There is no perfect architecture.

Examples:

~~~text
Monolith
→ simpler operations
→ broader deployment boundary

Microservices
→ independent boundaries
→ higher distributed-system complexity

Cache
→ lower latency
→ stale-data risk

Async queue
→ decoupling
→ eventual processing complexity
~~~

Engineering means choosing trade-offs intentionally.

---

# 38. Production Readiness Questions

Before deploying an application architecture, ask:

~~~text
How does traffic enter?
Where does state live?
What are the dependencies?
What happens when each dependency fails?
How do we scale?
How do we observe failures?
How do we recover?
What is the rollback path?
Where are single points of failure?
Who owns each component?
~~~

These are architecture and operations questions together.

---

# 39. Senior Engineer Perspective

A senior engineer should be able to draw:

~~~text
User
→ Entry Point
→ Application Components
→ Data Stores
→ Dependencies
~~~

Then explain:

- synchronous dependencies
- asynchronous paths
- state ownership
- failure points
- bottlenecks
- recent changes
- scaling limits

Senior troubleshooting is architecture-aware.

---

# 40. SRE Perspective

An SRE asks:

- what are the critical user journeys?
- which dependencies affect the SLI?
- where can latency accumulate?
- which failure should page?
- what can degrade gracefully?
- which queues can backlog?
- how do we detect saturation?
- what is the blast radius?

Example:

~~~text
Payment provider unavailable
       ↓
Can users still browse?
Can orders be queued?
Should checkout fail?
What SLO is affected?
~~~

Reliability depends on architecture behavior, not only infrastructure health.

---

# 41. Architect Perspective

An architect starts with requirements.

Questions include:

~~~text
How many users?
What latency target?
What availability target?
How much data?
How fast will traffic grow?
What consistency is required?
What recovery target?
What security boundaries?
What budget?
What team skills?
~~~

Only then choose patterns such as:

- monolith
- modular monolith
- microservices
- synchronous API
- asynchronous messaging
- cache
- replication
- load balancing

Architecture should follow requirements and constraints.

---

# 42. Common Beginner Mistakes

## Mistake 1

"Microservices are always better."

No. They trade simpler deployment boundaries for distributed-system complexity.

## Mistake 2

"Stateless means the system has no data."

No. It often means application instances do not hold unique persistent request/session state locally.

## Mistake 3

"Load balancer makes everything highly available."

No. Shared dependencies can still fail.

## Mistake 4

"API means HTTP endpoint."

HTTP APIs are common, but API means a software interface/contract more generally.

## Mistake 5

"Database is only storage."

It is also a dependency with latency, consistency, capacity and availability characteristics.

## Mistake 6

"More services means more scalable."

More services can increase operational overhead without solving the actual bottleneck.

---

# 43. Five-Level Explanation

## L1 — Foundation

Applications often consist of clients, servers and databases communicating with each other.

## L2 — Engineer

Architecture defines components, interfaces, data/state and request flows.

## L3 — Senior Engineer

Architecture determines failure propagation, bottlenecks, deployability, scaling boundaries and troubleshooting paths.

## L4 — SRE

Reliability depends on dependency behavior, state, queues, latency, failure domains and graceful degradation.

## L5 — Architect

Architecture is the disciplined selection of boundaries and interaction patterns based on requirements, constraints and trade-offs.

---

# 44. What You Must Retain

Before moving on, retain:

- client and server are interaction roles
- architecture defines components and communication boundaries
- frontend/backend/data are separate responsibilities
- monolith and microservices both have valid use cases
- APIs are contracts
- synchronous calls create waiting dependencies
- asynchronous communication can decouple work but adds complexity
- state placement affects scaling and failover
- stateless app instances can still depend on stateful systems
- database/cache/queue are architectural dependencies
- load balancing helps distribute traffic but does not eliminate all SPOFs
- dependency chains affect end-to-end latency and availability
- failure can propagate across services
- architecture creates operational trade-offs
- requirements should drive design

---

# 45. Practical Package — Next Layer

The practical package should include safe local exercises such as:

- trace a request through client → API → data
- run multiple simple app instances behind a local load balancer simulation
- demonstrate stateless vs local-state behavior
- create a controlled dependency slowdown and observe propagation
- create a simple asynchronous producer/consumer flow

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 46. Assessment Package — Pending

The assessment package should test:

- client/server roles
- three-tier architecture
- monolith vs microservices
- API contracts
- synchronous vs asynchronous behavior
- stateful vs stateless
- dependency chains
- failure propagation
- scaling trade-offs
- Senior/SRE/Architect reasoning

---

# 47. Visual Package — Pending

The visual package should include:

1. Client → Server → Data
2. Three-Tier Architecture
3. Monolith vs Microservices
4. Synchronous vs Asynchronous Communication
5. Stateful vs Stateless Scaling
6. Request Path & Failure Propagation

---

# 48. What Comes Next

After D00-T004 is completed, continue to:

## 00.05 — Infrastructure Foundations

That topic will connect applications to:

- physical infrastructure
- virtual machines
- compute
- storage
- networking
- environments
- resource provisioning

---

# 49. Sources & Evidence

Planned authoritative source families for verification:

- HTTP/API standards and official documentation
- cloud architecture guidance
- microservices architecture guidance from primary engineering sources
- distributed-systems references
- database/data architecture documentation
- messaging platform documentation
- load-balancer documentation

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: pending
- assessment package: pending
- visual package: pending

Detailed verification record:

- [D00-T004 Source Verification](../../../../docs/sources/D00/D00-T004-source-verification.md)

Verified nuances:

- client/server are interaction roles
- API is broader than HTTP
- stateless application instances can still depend on stateful systems
- microservices are not automatically better than monoliths
- load balancing alone does not guarantee high availability
- asynchronous communication and caching introduce their own operational trade-offs
