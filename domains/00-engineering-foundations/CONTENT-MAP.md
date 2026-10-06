# D00 Content Mapping

GitHub is the permanent knowledge base. Public content is the distribution and teach-back layer.

## Priorities

- **P1 Flagship** — deep video/article/lab/scenario
- **P2 Core** — standalone content
- **P3 Supporting** — micro lesson, short, diagram or section
- **P4 Reference** — documentation/cheat sheet

## Signature Series

- How It Really Works
- Why Does It Exist
- Under the Hood
- Follow the Request
- Build-Break-Fix
- Production Room
- Think Like an SRE
- Alert to RCA
- 5 Levels
- Architecture With Saqib
- Engineering Trade-Offs
- Real DevOps Interview
- Don't Do This in Prod
- Learn in Public

## D00-T001 — How Computers Work

Priority: **P1**

Visual package:

1. [Computer System Overview](../../docs/diagrams/D00/D00-T001/DIA-D00-001-computer-system-overview.md)
2. [Memory & Storage Hierarchy](../../docs/diagrams/D00/D00-T001/DIA-D00-002-memory-hierarchy.md)
3. [Application to Hardware Flow](../../docs/diagrams/D00/D00-T001/DIA-D00-003-application-to-hardware-flow.md)
4. [Bottleneck & Queueing Mental Model](../../docs/diagrams/D00/D00-T001/DIA-D00-004-bottleneck-queueing.md)
5. [Process & Resource Relationship](../../docs/diagrams/D00/D00-T001/DIA-D00-005-process-resource-relationship.md)

## D00-T002 — Operating System Mental Model

Priority: **P1**

Visual package:

1. [Operating System Overview](../../docs/diagrams/D00/D00-T002/DIA-D00-006-operating-system-overview.md)
2. [User Space, System Calls & Kernel Boundary](../../docs/diagrams/D00/D00-T002/DIA-D00-007-user-kernel-boundary.md)
3. [Process States & CPU Scheduling](../../docs/diagrams/D00/D00-T002/DIA-D00-008-process-states-scheduling.md)
4. [Application I/O Through the Kernel](../../docs/diagrams/D00/D00-T002/DIA-D00-009-application-io-kernel-flow.md)
5. [Virtual Machine vs Container OS Model](../../docs/diagrams/D00/D00-T002/DIA-D00-010-vm-vs-container.md)

These diagrams can later be reused in deep videos, Shorts, LinkedIn carousels, articles, practical explanations and teach-back material.


## D00-T003 — Software Engineering Foundations

Priority: **P1**

Visual package:

1. [Source to Process Lifecycle](../../docs/diagrams/D00/D00-T003/DIA-D00-011-source-to-process-lifecycle.md)
2. [Compiler vs Runtime-Driven Execution](../../docs/diagrams/D00/D00-T003/DIA-D00-012-compiler-vs-runtime.md)
3. [Dependency Graph](../../docs/diagrams/D00/D00-T003/DIA-D00-013-dependency-graph.md)
4. [Build-Time vs Runtime Dependencies](../../docs/diagrams/D00/D00-T003/DIA-D00-014-buildtime-vs-runtime-dependencies.md)
5. [Build Once, Promote the Artifact](../../docs/diagrams/D00/D00-T003/DIA-D00-015-build-once-promote.md)
6. [Build vs Startup vs Runtime Failure](../../docs/diagrams/D00/D00-T003/DIA-D00-016-failure-stage-model.md)

Recommended content angles:

- **How It Really Works:** Source Code to Production Process
- **Under the Hood:** Compiler vs Runtime
- **Build-Break-Fix:** Missing Configuration After a Green CI Build
- **5 Levels:** Explain an Artifact from Beginner to Architect
- **Production Room:** CI Passed but Production Failed


## D00-T004 — Application Architecture Fundamentals

Priority: **P1**

Visual package:

1. [Client → Server → Data](../../docs/diagrams/D00/D00-T004/DIA-D00-017-client-server-data.md)
2. [Three-Tier Architecture](../../docs/diagrams/D00/D00-T004/DIA-D00-018-three-tier-architecture.md)
3. [Monolith vs Microservices](../../docs/diagrams/D00/D00-T004/DIA-D00-019-monolith-vs-microservices.md)
4. [Synchronous vs Asynchronous Communication](../../docs/diagrams/D00/D00-T004/DIA-D00-020-sync-vs-async.md)
5. [Stateful vs Stateless Scaling](../../docs/diagrams/D00/D00-T004/DIA-D00-021-stateful-vs-stateless.md)
6. [Request Path & Failure Propagation](../../docs/diagrams/D00/D00-T004/DIA-D00-022-request-path-failure-propagation.md)

Recommended content angles:

- **Follow the Request:** Trace a User Request Through the Architecture
- **Architecture With Saqib:** Monolith vs Microservices Without Hype
- **Think Like an SRE:** Why a Healthy App Can Still Be Slow
- **Build-Break-Fix:** Local State Breaks Horizontal Scaling
- **5 Levels:** Explain Stateless Architecture from Beginner to Architect


## D00-T005 — Infrastructure Foundations

Priority: **P1**

Visual package:

1. [Physical Server Resource Model](../../docs/diagrams/D00/D00-T005/DIA-D00-023-physical-server-resource-model.md)
2. [Bare Metal vs Virtual Machine](../../docs/diagrams/D00/D00-T005/DIA-D00-024-bare-metal-vs-virtual-machine.md)
3. [Local vs Shared Storage](../../docs/diagrams/D00/D00-T005/DIA-D00-025-local-vs-shared-storage.md)
4. [Network Path: Client → Load Balancer → Compute](../../docs/diagrams/D00/D00-T005/DIA-D00-026-network-path-client-loadbalancer-compute.md)
5. [Failure Domains: Host → Rack → Zone → Region](../../docs/diagrams/D00/D00-T005/DIA-D00-027-failure-domains.md)
6. [Capacity, Headroom & Failover](../../docs/diagrams/D00/D00-T005/DIA-D00-028-capacity-headroom-failover.md)

Recommended content angles:

- **How It Really Works:** What Infrastructure Actually Means
- **Under the Hood:** Physical Host vs Virtual Machine
- **Follow the Request:** DNS → Load Balancer → Compute → Dependency
- **Think Like an SRE:** Why Two VMs May Still Share One Failure Domain
- **5 Levels:** Explain Capacity and Headroom from Beginner to Architect


## D00-T006 — Cloud Mental Models

Priority: **P1**

Visual package:

1. [Traditional Infrastructure vs Cloud Control Plane](../../docs/diagrams/D00/D00-T006/DIA-D00-029-traditional-vs-cloud-control-plane.md)
2. [Control Plane vs Data Plane](../../docs/diagrams/D00/D00-T006/DIA-D00-030-control-plane-vs-data-plane.md)
3. [IaaS vs PaaS vs SaaS Responsibility Stack](../../docs/diagrams/D00/D00-T006/DIA-D00-031-service-model-responsibility-stack.md)
4. [Region / Zone / Resource Failure Domains](../../docs/diagrams/D00/D00-T006/DIA-D00-032-region-zone-failure-domains.md)
5. [Elasticity & Autoscaling Loop](../../docs/diagrams/D00/D00-T006/DIA-D00-033-elasticity-autoscaling-loop.md)
6. [Cloud Responsibility / Cost / Governance Triangle](../../docs/diagrams/D00/D00-T006/DIA-D00-034-responsibility-cost-governance.md)

Recommended content angles:

- **How It Really Works:** Cloud Is More Than Someone Else's Server
- **Under the Hood:** Control Plane vs Data Plane During an Incident
- **Think Like an SRE:** Why Autoscaling Can Still Fail
- **Architecture With Saqib:** IaaS vs PaaS vs SaaS Responsibility Boundaries
- **5 Levels:** Explain Cloud Failure Domains from Beginner to Architect

## Rule

Research once, verify it, build the canonical topic, then repurpose it into the right formats without duplicating technical truth across multiple places.
