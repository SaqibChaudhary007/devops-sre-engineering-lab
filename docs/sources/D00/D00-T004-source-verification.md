# D00-T004 Source Verification — Application Architecture Fundamentals

## Verification Goal

Verify the core factual claims in **00.04 — Application Architecture Fundamentals** against standards, official cloud architecture guidance, and authoritative engineering references before treating the topic as DOC-VERIFIED.

## Verification Status

**Result:** Core claims verified.

**Evidence level:** E2 — documented by standards, official architecture guidance, and authoritative engineering references.

The topic intentionally teaches architecture mental models rather than prescribing one universal design.

## Verified Claim Map

| Topic claim | Verification | Source |
|---|---|---|
| HTTP is a stateless request/response application protocol with client/server semantics | Verified | RFC 9110 |
| N-tier architecture separates presentation/business/data responsibilities | Verified | Microsoft Azure Architecture Center |
| Microservices are independently deployable services organized around business capabilities and well-defined APIs | Verified | Microsoft Azure Architecture Center; Fowler/Lewis |
| Microservices add distributed-system and operational complexity | Verified | Microsoft Azure Architecture Center; Fowler/Lewis |
| Asynchronous/event-driven communication decouples producers and consumers but adds delivery/consistency challenges | Verified | Microsoft Azure Architecture Center |
| Stateless application instances are easier to horizontally scale and replace | Verified | AWS Well-Architected Framework |
| Load balancers distribute incoming traffic across multiple targets and can use health checks | Verified | AWS Elastic Load Balancing documentation |
| Cache-aside can reduce repeated data-store access but introduces consistency/staleness concerns | Verified | Microsoft Azure Architecture Center |
| Architecture style should be chosen from requirements and trade-offs rather than fashion | Verified | Microsoft Azure Architecture Center; Fowler references |
| Monoliths can be valid and microservices are not automatically the right starting point | Verified as authoritative engineering guidance | Martin Fowler |

## Primary / Authoritative Sources

### HTTP Semantics — RFC 9110

- https://www.rfc-editor.org/rfc/rfc9110.html

Supports:

- request/response semantics
- client/server roles
- HTTP as a stateless application-level protocol
- methods, headers, status codes and representations

Important nuance: the topic's "API" concept is broader than HTTP. HTTP is used only as a common example.

### Microsoft Azure Architecture Center — Architecture Styles

- https://learn.microsoft.com/azure/architecture/guide/architecture-styles
- https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices
- https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven
- https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/web-queue-worker

Supports:

- N-tier/layered architecture
- microservice architecture
- asynchronous messaging
- event producers/consumers
- independent scaling
- distributed-system challenges
- architecture-style trade-offs

### AWS Well-Architected — Stateless Systems

- https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_mitigate_interaction_failure_stateless.html

Supports:

- stateless application design
- horizontal scaling
- replacing individual compute instances
- externalizing session/state where appropriate

Important nuance: stateless application instances do not mean the entire system contains no state.

### AWS Elastic Load Balancing

- https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html

Supports:

- distributing incoming traffic across multiple targets
- health checks
- routing away from unhealthy targets
- scaling compute targets behind a load balancer

Important nuance: a load balancer does not eliminate shared downstream failure points.

### Microsoft Azure Architecture Center — Cache-Aside

- https://learn.microsoft.com/azure/architecture/patterns/cache-aside
- https://learn.microsoft.com/en-us/azure/architecture/best-practices/caching

Supports:

- cache lookup before data-store access
- cache misses
- loading data on demand
- performance benefits
- stale-data/consistency trade-offs

### Martin Fowler / James Lewis — Microservices

- https://martinfowler.com/articles/microservices.html
- https://martinfowler.com/bliki/MonolithFirst.html
- https://martinfowler.com/articles/microservice-trade-offs.html

Supports the authoritative engineering guidance that:

- microservices are independently deployable services
- remote calls add cost/complexity compared with in-process calls
- service boundaries matter
- monoliths can be valid
- microservices impose an operational premium
- architecture choice depends on context and capability

## Verified Nuances / Corrections

### 1. Client and Server Are Roles

A component can act as a server to one caller and a client to another dependency.

### 2. API Is Broader Than HTTP

HTTP APIs are common, but an API is a software interface/contract, not merely a URL or HTTP endpoint.

### 3. "Stateless" Does Not Mean "No State"

A stateless application tier can still rely on:

- databases
- distributed caches
- object storage
- queues

The useful distinction is whether any instance owns unique local state needed for future requests.

### 4. Microservices Are Not Automatically Better

Microservices improve some deployment and scaling boundaries but introduce distributed-system complexity, observability needs, data-consistency challenges and operational overhead.

### 5. Monolith Does Not Mean Poor Architecture

A well-structured modular monolith can have clear internal boundaries and lower operational complexity.

### 6. Load Balancing Is Not High Availability by Itself

Availability still depends on downstream systems, failure domains, health checks, state and redundant capacity.

### 7. Asynchronous Communication Trades Immediate Coupling for Operational Complexity

Queues/brokers can buffer and decouple work but require reasoning about:

- retries
- ordering
- duplicate handling
- backlog
- eventual processing
- failure recovery

### 8. Caches Are Additional State

A cache may improve latency and reduce backend load but introduces invalidation and consistency concerns.

## Evidence Decision

The following D00-T004 areas are now eligible for **DOC-VERIFIED** status:

- client/server request-response model
- HTTP example
- N-tier / three-tier architecture
- microservices mental model and trade-offs
- synchronous vs asynchronous communication
- stateless scaling principle
- load balancing principle
- cache-aside mental model
- architecture trade-off framing

## Not Yet LAB-VERIFIED

The following still require controlled hands-on execution:

- tracing a request through client → API → data
- comparing multiple stateless app instances
- demonstrating local-state/session stickiness problems
- creating a controlled dependency slowdown and observing latency propagation
- demonstrating asynchronous producer/consumer behavior

Those become the D00-T004 practical package.
