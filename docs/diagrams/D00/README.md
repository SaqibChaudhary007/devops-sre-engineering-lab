# D00 Diagrams

Visual assets for Domain 00.

## D00-T001 — How Computers Work

- [Visual / Diagram Package](D00-T001/README.md)

Includes:

- Computer System Overview
- Memory & Storage Hierarchy
- Application to Hardware Flow
- Bottleneck & Queueing Mental Model
- Process & Resource Relationship

## D00-T002 — Operating System Mental Model

- [Visual / Diagram Package](D00-T002/README.md)

Includes:

- Operating System Overview
- User Space, System Calls & Kernel Boundary
- Process States & CPU Scheduling
- Application I/O Through the Kernel
- Virtual Machine vs Container OS Model

Mermaid is used for the initial visual system because it renders directly in GitHub, remains editable in source control and supports reuse across the curriculum.


## D00-T003 — Software Engineering Foundations

- [Visual / Diagram Package](D00-T003/README.md)

Includes:

- Source to Process Lifecycle
- Compiler vs Runtime-Driven Execution
- Dependency Graph
- Build-Time vs Runtime Dependencies
- Build Once, Promote the Artifact
- Build vs Startup vs Runtime Failure


## D00-T004 — Application Architecture Fundamentals

- [Visual / Diagram Package](D00-T004/README.md)

Includes:

- Client → Server → Data
- Three-Tier Architecture
- Monolith vs Microservices
- Synchronous vs Asynchronous Communication
- Stateful vs Stateless Scaling
- Request Path & Failure Propagation


## D00-T005 — Infrastructure Foundations

- [Visual / Diagram Package](D00-T005/README.md)

Includes:

- Physical Server Resource Model
- Bare Metal vs Virtual Machine
- Local vs Shared Storage
- Network Path: Client → Load Balancer → Compute
- Failure Domains: Host → Rack → Zone → Region
- Capacity, Headroom & Failover


## D00-T006 — Cloud Mental Models

- [Visual / Diagram Package](D00-T006/README.md)

Includes:

- Traditional Infrastructure vs Cloud Control Plane
- Control Plane vs Data Plane
- IaaS vs PaaS vs SaaS Responsibility Stack
- Region / Zone / Resource Failure Domains
- Elasticity & Autoscaling Loop
- Cloud Responsibility / Cost / Governance Triangle


## D00-T007 — DevOps Foundations

- [Visual / Diagram Package](D00-T007/README.md)

Includes:

- Traditional Siloed Delivery vs DevOps Flow
- Idea → Production → Feedback Loop
- Queue / Handoff / Bottleneck Model
- CI vs Continuous Delivery vs Continuous Deployment
- Delivery Performance: Throughput, Instability & Recovery
- DevOps vs SRE vs Platform Engineering


## D00-T008 — Infrastructure as Code Mental Model

- [Visual / Diagram Package](D00-T008/README.md)

Includes:

- Manual Infrastructure vs Infrastructure as Code
- Desired State vs Actual State
- Declarative vs Imperative
- Plan → Apply → Infrastructure Lifecycle
- IaC State / Dependency / Locking Model
- IaC Change Risk: Review → Blast Radius → Recovery


## D00-T009 — CI/CD Mental Model

- [Visual / Diagram Package](D00-T009/README.md)

Includes:

- CI vs Continuous Delivery vs Continuous Deployment
- Source → Build → Validate → Artifact → Promote → Deploy
- Build Once / Promote Same Artifact
- Pipeline Feedback & Failure Loop
- Deployment vs Release
- CI/CD + IaC + GitOps Relationship


## D00-T010 — Containers & Orchestration Mental Model

- [Visual / Diagram Package](D00-T010/README.md)

Includes:

- Virtual Machine vs Container
- Image → Container → Runtime → Host
- Image Layers + Writable Container Layer
- Desired Replicas → Scheduler → Nodes → Reconciliation
- Service Discovery + Load Balancing Across Replicas
- Container Failure vs Node Failure vs Orchestrator Recovery


## D00-T011 — Distributed Systems Foundations

- [Visual / Diagram Package](D00-T011/README.md)

Includes:

- Local Call vs Network Call
- Partial Failure & Ambiguous Timeout
- Retry → Duplicate → Idempotency Key
- Replication → Lag → Stale Read
- Partition Trade-Off / CAP Mental Model
- Timeout + Retry + Backoff + Circuit Breaker Failure Loop


## D00-T012 — Reliability Engineering Foundations

- [Visual / Diagram Package](D00-T012/README.md)

Includes:

- Reliability vs Availability vs Durability vs Resilience
- User Journey → Dependency Chain → Reliability Outcome
- Failure Domain → Blast Radius → Redundancy Placement
- Detect → Contain → Recover → Validate → Learn
- SLI → SLO → Error Budget Mental Model
- Capacity Headroom → Failure → Failover / Degradation


## D00-T013 — SRE Foundations

- [Visual / Diagram Package](D00-T013/README.md)

Includes:

- User Journey → SLI → SLO → Error Budget → Decision
- Page vs Ticket vs Dashboard
- Incident: Detect → Mitigate → Recover → Learn
- Toil → Automation → Engineering Capacity
- Error Budget → Change Velocity / Reliability Trade-Off
- Production Readiness → Operate → Incident → Improvement


## D00-T014 — Observability Foundations

- [Visual / Diagram Package](D00-T014/README.md)

Includes:

- System → Instrumentation → Telemetry → Correlation → Insight
- Metrics vs Logs vs Traces vs Events
- User Journey → Trace → Spans → Logs / Metrics
- RED vs USE vs Golden Signals
- Change Marker → Symptom → Dependency → Root-Cause Hypothesis
- Cardinality / Sampling / Retention / Cost Trade-Off
