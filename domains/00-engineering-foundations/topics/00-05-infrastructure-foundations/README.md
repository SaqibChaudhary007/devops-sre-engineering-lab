---
id: D00-T005
domain: D00
title: Infrastructure Foundations
level:
  - L1
  - L2
  - L3
priority: P1
status: published
estimated_time:
  theory: 5-7h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
    - D00-T003
    - D00-T004
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Under the Hood
  - Follow the Request
  - Five Levels
  - Architecture With Saqib
---

# 00.05 — Infrastructure Foundations

## Start Here

In the previous topics, you built the mental model from computer resources to operating systems, software, and application architecture.

Now we connect applications to the infrastructure they run on.

The core question is:

> What physical and virtual resources must exist so an application can run, communicate, persist data, scale, and recover?

Infrastructure is not only "servers."

It includes compute, memory, storage, networking, identity, environments, virtualization, capacity, failure domains, and the operational systems that keep workloads available.

This topic stays at the foundation level. Deep cloud, Linux, networking, storage, Kubernetes, IaC, and platform implementation come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- physical server vs virtual machine
- compute, memory, storage, and network as infrastructure resources
- host, guest, and hypervisor
- bare metal
- virtualization
- virtual CPU and memory
- local storage vs shared/remote storage
- block, file, and object storage at a high level
- IP address, subnet, route, firewall, and load balancer at a high level
- data center, rack, zone, and region as failure/location concepts
- environment separation
- resource provisioning
- capacity vs utilization
- vertical vs horizontal infrastructure scaling
- redundancy
- high availability
- fault domain
- single point of failure
- infrastructure dependency chains
- immutable vs mutable infrastructure at a high level
- why manual infrastructure changes create risk
- why infrastructure as code emerged
- why cloud is an operating model, not "someone else's server" only
- how infrastructure design affects reliability, security, performance, and cost

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)
- [00.04 — Application Architecture Fundamentals](../00-04-application-architecture-fundamentals/README.md)

You should already understand:

- CPU, memory, storage, and network
- operating system and processes
- runtime and artifact
- application dependencies
- request path
- state
- load balancing
- failure propagation

---

# Learning Package Navigation

Use this page as the canonical learner entry point.

Move through the package in this order:

1. **Learn** — complete the conceptual sections on this page.
2. **Verify** — review the [D00-T005 Source Verification](../../../../docs/sources/D00/D00-T005-source-verification.md).
3. **Visualize** — review the [D00-T005 Visual Package](../../../../docs/diagrams/D00/D00-T005/README.md).
4. **Observe Resources** — complete [OBS-D00-008 — Inspect Compute, Memory, Storage, and Network Resources](../../../../labs/observation/D00/OBS-D00-008-inspect-infrastructure-resources.md).
5. **Observe Virtualization & Failure Domains** — complete [OBS-D00-009 — Detect Virtualization and Map Infrastructure Dependencies](../../../../labs/observation/D00/OBS-D00-009-detect-virtualization-map-dependencies.md).
6. **Experiment with Capacity** — complete [EXP-D00-006 — Capacity, Utilization, and Headroom with a Bounded Workload](../../../../labs/experiments/D00/EXP-D00-006-capacity-utilization-headroom.md).
7. **Assess** — complete the [D00-T005 Assessment Package](../../../../assessments/topics/D00/D00-T005/README.md).
8. **Teach Back** — explain infrastructure at Beginner, Engineer, Senior, SRE, and Architect levels.
9. **Continue** — move to 00.06 only after the completion gate is satisfied.

## Visual Package

The dedicated diagrams are:

- [DIA-D00-023 — Physical Server Resource Model](../../../../docs/diagrams/D00/D00-T005/DIA-D00-023-physical-server-resource-model.md)
- [DIA-D00-024 — Bare Metal vs Virtual Machine](../../../../docs/diagrams/D00/D00-T005/DIA-D00-024-bare-metal-vs-virtual-machine.md)
- [DIA-D00-025 — Local vs Shared Storage](../../../../docs/diagrams/D00/D00-T005/DIA-D00-025-local-vs-shared-storage.md)
- [DIA-D00-026 — Network Path: Client → Load Balancer → Compute](../../../../docs/diagrams/D00/D00-T005/DIA-D00-026-network-path-client-loadbalancer-compute.md)
- [DIA-D00-027 — Failure Domains: Host → Rack → Zone → Region](../../../../docs/diagrams/D00/D00-T005/DIA-D00-027-failure-domains.md)
- [DIA-D00-028 — Capacity, Headroom & Failover](../../../../docs/diagrams/D00/D00-T005/DIA-D00-028-capacity-headroom-failover.md)

## Practical Package

- [OBS-D00-008 — Inspect Compute, Memory, Storage, and Network Resources](../../../../labs/observation/D00/OBS-D00-008-inspect-infrastructure-resources.md)
- [OBS-D00-009 — Detect Virtualization and Map Infrastructure Dependencies](../../../../labs/observation/D00/OBS-D00-009-detect-virtualization-map-dependencies.md)
- [EXP-D00-006 — Capacity, Utilization, and Headroom with a Bounded Workload](../../../../labs/experiments/D00/EXP-D00-006-capacity-utilization-headroom.md)

The practical assets remain **DRAFT** until they are executed end-to-end and promoted to `LAB-VERIFIED`.

## Assessment Package

The [D00-T005 Assessment Package](../../../../assessments/topics/D00/D00-T005/README.md) includes:

- 68-question knowledge check
- applied infrastructure/failure-domain scenario
- Senior/SRE/Architect follow-ups
- teach-back assessment
- scoring rubric
- remediation map

---

# 3. The Infrastructure Mental Model

A simplified system:

~~~text
Users
  ↓
Network
  ↓
Compute
  ↓
Operating System
  ↓
Application
  ↓
Storage / Database / Dependencies
~~~

Infrastructure supplies the environment in which software executes.

At a high level:

~~~text
Infrastructure
=
Compute
+ Memory
+ Storage
+ Network
+ Identity / Access
+ Availability / Failure Design
~~~

---

# 4. Physical Infrastructure

Physical infrastructure includes real hardware.

Examples:

- servers
- CPU
- RAM
- disks
- network interface cards
- switches
- routers
- racks
- power supplies
- cooling systems

A physical server is a computer designed to run workloads reliably.

Conceptually:

~~~text
Physical Server
├── CPU
├── Memory
├── Storage
└── Network Interfaces
~~~

---

# 5. Bare Metal

For this topic, a bare-metal workload means the general-purpose operating system/workload runs directly on physical hardware rather than inside a virtual machine.

Important nuance: some hypervisors also run directly on physical hardware, so "bare metal" is an industry term whose exact usage depends on context.

~~~text
Application
   ↓
Operating System
   ↓
Physical Hardware
~~~

Potential advantages:

- direct hardware access
- predictable performance
- no hypervisor layer
- useful for specialized workloads

Potential disadvantages:

- slower provisioning
- lower resource flexibility
- hardware lifecycle management
- capacity fragmentation

Bare metal is not "old technology." It is a deployment model with trade-offs.

---

# 6. Virtualization

Virtualization allows multiple isolated virtual machines to share one physical host.

~~~text
Physical Server
      ↓
Hypervisor
  ┌────┼────┐
  ↓    ↓    ↓
 VM1  VM2  VM3
~~~

Each VM generally has:

- virtual CPU
- virtual memory
- virtual disks
- virtual network interfaces
- its own guest operating system

Virtualization improved infrastructure utilization and provisioning flexibility.

---

# 7. Hypervisor

A hypervisor manages virtual machines and mediates access to physical resources.

Conceptually:

~~~text
VM
 ↓
Virtual Hardware
 ↓
Hypervisor
 ↓
Physical Hardware
~~~

The hypervisor is responsible for things such as:

- CPU scheduling
- memory allocation
- virtual device presentation
- isolation
- VM lifecycle

Deep hypervisor internals are outside D00.

---

# 8. Host and Guest

In virtualization:

## Host

The physical system and virtualization layer providing resources.

## Guest

The virtual machine consuming those resources.

Example:

~~~text
Physical Host
 ├── Guest VM A
 ├── Guest VM B
 └── Guest VM C
~~~

A failure in the host can affect multiple guests.

That is an important failure-domain concept.

---

# 9. Virtual CPU

A virtual CPU (vCPU) is a virtualized CPU resource presented to a VM.

Example:

~~~text
Physical CPU Capacity
        ↓
Hypervisor Scheduling
        ↓
vCPU assigned to VM
~~~

A vCPU is not automatically equal to one dedicated physical core.

The actual relationship depends on virtualization configuration and scheduling.

---

# 10. Virtual Memory

A VM is assigned a quantity of memory.

~~~text
Physical RAM
    ↓
Hypervisor
    ↓
VM Memory
~~~

If many VMs compete for memory, infrastructure behavior can affect workload performance.

At D00 level, remember:

> Application memory problems can originate at application, OS, container, VM, or host level.

---

# 11. Storage Foundations

Applications need storage for different purposes.

Examples:

- operating system files
- application binaries
- logs
- database files
- backups
- user content

A simple model:

~~~text
Application
  ↓
Filesystem / Storage Interface
  ↓
Storage System
~~~

Different storage types solve different problems.

---

# 12. Local Storage

Local storage is attached directly to or closely coupled with the compute instance.

Potential benefits:

- low latency
- simple path
- high performance

Potential limitations:

- data may be tied to one machine
- failover can be harder
- replacement may lose local data unless replicated/backed up

---

# 13. Shared / Remote Storage

Remote/shared storage is accessed over a network or shared fabric.

~~~text
Compute A ─┐
Compute B ─┼→ Shared Storage
Compute C ─┘
~~~

Potential benefits:

- data survives compute replacement
- multiple systems may access storage
- easier centralized management

Potential trade-offs:

- network dependency
- latency
- shared bottleneck
- failure-domain complexity

---

# 14. Block Storage — Introductory View

Block storage presents raw storage volumes to a system.

Conceptually:

~~~text
Virtual / Physical Disk
        ↓
Blocks
        ↓
Filesystem or Database
~~~

Common use cases include:

- VM disks
- database volumes
- filesystems

Deep storage design comes later.

---

# 15. File Storage — Introductory View

File storage exposes files and directories.

~~~text
Client
  ↓
Shared Filesystem
  ↓
Files / Directories
~~~

It is useful when multiple systems need file-oriented access.

Examples conceptually:

- shared application files
- user home directories
- shared content

---

# 16. Object Storage — Introductory View

Object storage stores data as objects accessed through an API.

Conceptually:

~~~text
Application
   ↓ API
Object Storage
   ↓
Object + Metadata
~~~

Common use cases:

- images
- backups
- logs
- archives
- static assets

Object storage is not mounted filesystem storage by default in the same sense as block/file systems.

---

# 17. Networking Foundations

Infrastructure networking connects systems.

At a high level:

~~~text
Client
  ↓
Network
  ↓
Server
~~~

Networking infrastructure includes concepts such as:

- IP address
- subnet
- route
- gateway
- firewall
- load balancer
- DNS

Deep networking belongs to D02.

---

# 18. IP Address

An IP address identifies a network interface/location in an IP network.

Example concept:

~~~text
Application Server
IP: 10.0.1.10
~~~

Applications do not communicate with "server names" magically.

Names are resolved to network addresses through systems such as DNS.

---

# 19. Subnet

A subnet groups IP addresses into a network range.

Conceptually:

~~~text
10.0.1.0/24
├── 10.0.1.10
├── 10.0.1.11
└── 10.0.1.12
~~~

Subnets help organize and control network communication.

---

# 20. Routing

Routing determines where network traffic should go next.

~~~text
Source Network
   ↓
Router / Route Table
   ↓
Destination Network
~~~

If a route does not exist or points incorrectly, systems may be healthy but unable to communicate.

---

# 21. Firewall / Network Policy Mental Model

A firewall controls allowed and denied traffic.

Conceptually:

~~~text
Source
  ↓
Firewall Rule
  ↓
Allowed? → Destination
Denied?  → Drop / Reject
~~~

A firewall problem can look like an application problem.

This is why infrastructure troubleshooting must follow the request path.

---

# 22. Load Balancer as Infrastructure

A load balancer distributes traffic across backend instances.

~~~text
Users
  ↓
Load Balancer
  ↓
┌────────┬────────┬────────┐
│ App A  │ App B  │ App C  │
└────────┴────────┴────────┘
~~~

At infrastructure level, a load balancer is part of the traffic-entry and availability design.

It depends on:

- networking
- health checks
- backend reachability
- capacity
- configuration

---

# 23. Data Center

A data center is a physical facility containing compute, network, storage, power, and cooling infrastructure.

Failure risks may include:

- power loss
- network loss
- cooling problems
- hardware failures
- physical incidents

Modern architecture often tries to avoid placing all critical capacity in one failure location.

---

# 24. Rack as a Failure Domain

Servers may share physical dependencies in a rack.

Examples:

- top-of-rack switch
- power distribution
- physical location

If every redundant server sits in one rack, redundancy may be weaker than it appears.

This introduces the concept of failure domains.

---

# 25. Failure Domain

A failure domain is a group of resources that can fail together because they share a dependency.

Examples:

~~~text
same physical host
same rack
same switch
same power feed
same zone
same region
~~~

High availability requires understanding what can fail together.

---

# 26. Zone and Region — Introductory View

Cloud platforms commonly organize infrastructure into regions and zones.

Conceptually:

~~~text
Region
 ├── Zone A
 ├── Zone B
 └── Zone C
~~~

Exact provider definitions differ.

At D00 level:

- region = larger geographic/operational area
- zone = more isolated failure location within/around a region

Deep AWS/Azure/GCP behavior belongs later.

---

# 27. Environment Separation

Organizations commonly separate environments.

Examples:

~~~text
Development
Testing
QA
Staging
Production
~~~

Why?

- reduce production risk
- validate changes
- control access
- isolate data/configuration
- support testing

But duplicated environments also add:

- cost
- configuration drift
- operational overhead

---

# 28. Resource Provisioning

Provisioning means creating or allocating infrastructure resources.

Examples:

- VM
- disk
- network
- firewall rule
- load balancer
- DNS record

Manual provisioning often looks like:

~~~text
Ticket
→ Human Login
→ Click / Command
→ Resource Created
~~~

Automation changes this model.

---

# 29. Manual Infrastructure Risk

Manual infrastructure changes can create:

- inconsistent configuration
- undocumented changes
- slow recovery
- environment drift
- audit difficulty
- dependency on individual knowledge

This is one reason infrastructure automation and IaC became important.

---

# 30. Mutable Infrastructure

Mutable infrastructure changes existing systems in place.

Example:

~~~text
Existing Server
  ↓
Install package
  ↓
Edit config
  ↓
Restart service
~~~

This can be valid, but repeated manual mutation can accumulate hidden state and drift.

---

# 31. Immutable Infrastructure — Introductory View

Immutable infrastructure emphasizes replacing rather than continuously modifying deployed instances.

Conceptually:

~~~text
Old Image / Instance
      ↓
Create New Version
      ↓
Deploy New Instance
      ↓
Replace Old
~~~

Potential benefits:

- repeatability
- easier rollback
- less drift
- clearer version identity

It is a principle, not a universal requirement.

---

# 32. Infrastructure as Code — Preview

Infrastructure as Code expresses desired infrastructure in files/code that can be versioned and reviewed.

~~~text
Infrastructure Definition
        ↓
Automation Tool
        ↓
Infrastructure Resources
~~~

Benefits may include:

- repeatability
- review
- version history
- automation
- reproducibility
- reduced manual drift

Deep IaC belongs to D18.

---

# 33. Capacity

Capacity is how much work/resources a system can support.

Examples:

- CPU capacity
- memory capacity
- disk capacity
- network bandwidth
- IOPS
- connection capacity

A system can be healthy now but still have insufficient headroom for growth or spikes.

---

# 34. Utilization

Utilization is how much of a resource is being used.

Example:

~~~text
Capacity: 100 units
Used:      70 units
Utilization: 70%
~~~

High utilization does not always mean failure.

Low utilization does not always mean healthy.

You must understand:

- saturation
- queues
- latency
- workload pattern

---

# 35. Headroom

Headroom is unused capacity reserved for:

- traffic growth
- failover
- spikes
- maintenance
- unexpected load

Example:

~~~text
Normal traffic uses 60%
40% remains as headroom
~~~

If one instance fails, remaining infrastructure may need enough headroom to carry the load.

---

# 36. Vertical Infrastructure Scaling

Vertical scaling increases resources on one system.

~~~text
VM:
4 vCPU / 8 GB
      ↓
8 vCPU / 32 GB
~~~

Advantages:

- simple mental model
- fewer instances

Trade-offs:

- finite limit
- larger failure impact
- resize/restart requirements
- potentially higher cost

---

# 37. Horizontal Infrastructure Scaling

Horizontal scaling adds more instances.

~~~text
1 VM
 ↓
3 VMs
~~~

Potential benefits:

- more capacity
- redundancy
- easier maintenance/failover

But horizontal scaling requires architecture that can distribute work/state correctly.

---

# 38. Redundancy

Redundancy means having additional capacity/components so one failure does not necessarily stop the service.

Example:

~~~text
Load Balancer
  ↓
App A
App B
~~~

If App A fails, App B may continue serving traffic.

But redundancy must span meaningful failure domains.

Two VMs on the same failed physical host may not provide true resilience.

---

# 39. High Availability

High availability is a system property aimed at minimizing service interruption.

It can involve:

- redundancy
- health checks
- failover
- load balancing
- replicated state
- multiple failure domains
- recovery automation

Important:

> High availability is not achieved by adding duplicates blindly.

The whole dependency path matters.

---

# 40. Infrastructure Dependency Chain

Consider:

~~~text
Application
  ↓
VM
  ↓
Hypervisor
  ↓
Physical Host
  ↓
Rack Network
  ↓
Storage
  ↓
Data Center Power
~~~

A problem at a lower layer can appear as an application outage.

This is why production troubleshooting must connect software symptoms to infrastructure layers.

---

# 41. Cloud Mental Model — Preview

Cloud platforms provide infrastructure through APIs and managed control planes.

Conceptually:

~~~text
Infrastructure Request
      ↓
Cloud API / Control Plane
      ↓
Compute / Network / Storage Resource
~~~

Cloud changes provisioning speed, abstraction, automation, billing, and responsibility models.

It does not eliminate infrastructure fundamentals.

Deep cloud comes in D06, AWS D16, and Azure D17.

---

# 42. Shared Responsibility — Preview

In hosted/cloud environments, responsibilities are divided between provider and customer.

Examples vary by service model.

At a high level:

~~~text
Provider
→ physical facilities / platform layers

Customer
→ workload configuration / identity / data / application responsibilities
~~~

Exact boundaries depend on the service.

---

# 43. Security Perspective

Infrastructure security includes:

- access control
- network segmentation
- patching
- encryption
- secrets
- hardening
- auditability
- least privilege

A secure application on insecure infrastructure is still insecure.

---

# 44. Performance Perspective

Infrastructure affects application performance through:

- CPU scheduling
- memory pressure
- storage latency
- network latency
- bandwidth
- noisy-neighbor effects
- virtualization overhead
- capacity limits

Do not assume every performance problem is inside application code.

---

# 45. Cost Perspective

Infrastructure has cost.

Typical drivers include:

- compute size
- number of instances
- storage
- network transfer
- redundancy
- managed services
- backup/retention
- idle capacity

Architecture decisions always have cost consequences.

---

# 46. Senior Engineer Perspective

A senior engineer asks:

~~~text
Where does the workload run?
What are its compute/memory/storage requirements?
Where does state live?
How does traffic reach it?
Which infrastructure dependencies exist?
What is the failure domain?
What happens if one instance/host/zone fails?
How much headroom exists?
What changed recently?
~~~

The goal is to connect application behavior to infrastructure reality.

---

# 47. SRE Perspective

An SRE thinks in terms of:

- availability
- latency
- errors
- traffic
- saturation
- capacity
- failure domains
- recovery time
- redundancy

Example:

~~~text
One host fails
    ↓
Multiple VMs disappear
    ↓
Remaining capacity saturates
    ↓
Latency rises
    ↓
Error rate rises
~~~

Infrastructure design directly affects SLO performance.

---

# 48. Architect Perspective

An architect starts with requirements and constraints.

Questions include:

- expected traffic
- performance targets
- availability target
- data durability
- recovery requirements
- compliance
- geography
- cost
- team capability
- operational complexity

Then infrastructure patterns are selected.

Examples:

- bare metal vs VM
- local vs shared storage
- single vs multiple failure domains
- vertical vs horizontal scaling
- self-managed vs managed service
- mutable vs immutable approach

---

# 49. Common Beginner Mistakes

## Mistake 1

"Infrastructure means server."

Infrastructure includes compute, storage, networking, identity, availability design, and physical/platform dependencies.

## Mistake 2

"VM is a physical machine."

A VM is a virtualized compute environment backed by physical infrastructure.

## Mistake 3

"Two servers mean high availability."

Not if both share the same critical failure domain.

## Mistake 4

"Low CPU means infrastructure is healthy."

Storage, network, memory, queues, dependency latency, or saturation can still be the issue.

## Mistake 5

"Cloud removes infrastructure problems."

Cloud changes how infrastructure is consumed and operated; it does not remove failure, capacity, security, or cost concerns.

## Mistake 6

"Automation means zero human judgment."

Automation reduces repetitive manual work, but design, validation, risk decisions, and incident judgment still matter.

---

# 50. Five-Level Explanation

## L1 — Foundation

Infrastructure is the compute, memory, storage, and networking that software needs to run.

## L2 — Engineer

Applications run on physical or virtual resources connected through networks and storage systems.

## L3 — Senior Engineer

Infrastructure design determines capacity, failure domains, state placement, scaling options, and troubleshooting boundaries.

## L4 — SRE

Reliability depends on redundancy, headroom, failure-domain isolation, recovery behavior, and measurable saturation.

## L5 — Architect

Infrastructure architecture balances performance, availability, security, cost, operability, compliance, and organizational capability.

---

# 51. What You Must Retain

Before moving on, retain:

- physical infrastructure underpins virtual infrastructure
- VMs share physical hosts through a virtualization layer
- compute, memory, storage, and network are all infrastructure resources
- storage can be local or remote/shared
- block, file, and object storage solve different access patterns
- networking determines reachability
- infrastructure can fail in shared failure domains
- redundancy is meaningful only when failure domains are understood
- utilization is not the same as capacity or saturation
- headroom matters for spikes and failover
- infrastructure changes can drift when managed manually
- automation and IaC improve repeatability
- high availability depends on the whole dependency chain
- cloud does not eliminate infrastructure fundamentals
- infrastructure decisions affect reliability, security, performance, and cost

---

# 52. Practical Package

Complete the practical assets:

1. [OBS-D00-008 — Inspect Compute, Memory, Storage, and Network Resources](../../../../labs/observation/D00/OBS-D00-008-inspect-infrastructure-resources.md)
2. [OBS-D00-009 — Detect Virtualization and Map Infrastructure Dependencies](../../../../labs/observation/D00/OBS-D00-009-detect-virtualization-map-dependencies.md)
3. [EXP-D00-006 — Capacity, Utilization, and Headroom with a Bounded Workload](../../../../labs/experiments/D00/EXP-D00-006-capacity-utilization-headroom.md)

These assets turn infrastructure abstractions into observable guest-visible evidence, failure-domain reasoning, and capacity/headroom behavior.

---

# 53. Assessment Package

Complete the [D00-T005 Assessment Package](../../../../assessments/topics/D00/D00-T005/README.md).

It tests:

- physical vs virtual infrastructure
- hypervisor, host, and guest
- compute/memory/storage/network
- storage access models
- network foundations
- failure domains
- environment separation
- provisioning
- mutable vs immutable infrastructure
- capacity/utilization/headroom
- scaling
- HA/redundancy
- Senior/SRE/Architect reasoning

---

# 54. Visual Package

Review the [D00-T005 Visual Package](../../../../docs/diagrams/D00/D00-T005/README.md).

The package includes:

1. Physical Server Resource Model
2. Bare Metal vs Virtual Machine
3. Local vs Shared Storage
4. Network Path: Client → Load Balancer → Compute
5. Failure Domains: Host → Rack → Zone → Region
6. Capacity, Headroom & Failover

---

# 55. Completion Gate

Before moving on, confirm that you can:

- explain physical vs virtual infrastructure
- explain host, guest, hypervisor, and vCPU
- distinguish local, shared, block, file, and object storage at a high level
- trace a network path through interface, route, firewall, and load balancer concepts
- explain why two VMs may still share one failure domain
- explain host/rack/zone/region failure-domain thinking without assuming provider-specific details
- distinguish capacity, utilization, saturation, and headroom
- explain why low CPU does not prove infrastructure health
- explain why failover capacity must include storage, network, database, and dependency limits
- explain redundancy vs high availability
- explain mutable vs immutable infrastructure
- explain what IaC improves and what it does not guarantee
- separate observed, inferred, and unknown infrastructure facts
- complete the practical package
- score at least 80% on the knowledge check
- demonstrate at least L3 / FD-3 reasoning
- teach the infrastructure mental model clearly without relying on notes

# 56. What Comes Next

After D00-T005 is completed, continue to:

## 00.06 — Cloud Mental Models

That topic will connect infrastructure fundamentals to:

- on-demand provisioning
- cloud control planes
- service models
- elasticity
- shared responsibility
- regions/zones
- managed services
- consumption and cost models

---

# 57. Sources & Evidence

Planned authoritative source families for verification:

- virtualization/hypervisor documentation
- Linux/kernel/system documentation
- storage architecture documentation
- networking standards/documentation
- AWS/Azure/GCP infrastructure architecture guidance
- reliability/failure-domain guidance
- infrastructure-as-code documentation
- cloud shared-responsibility documentation

Current evidence status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- source verification: complete
- practical package: authored as DRAFT; LAB-VERIFICATION pending
- assessment package: authored and cross-linked
- visual package: authored and cross-linked
- canonical learner journey: integrated

Detailed verification record:

- [D00-T005 Source Verification](../../../../docs/sources/D00/D00-T005-source-verification.md)

Verified nuances:

- vCPU is an abstraction and does not always mean one dedicated physical core
- local storage persistence depends on platform lifecycle guarantees
- block, file, and object describe different storage access models
- failure-domain redundancy must account for shared host/rack/zone dependencies
- region/zone semantics differ across providers
- redundancy alone does not guarantee high availability
- utilization and saturation are different concepts
- immutable infrastructure and IaC are operating patterns, not automatic correctness
- shared-responsibility boundaries vary by service model


## Topic Package Status

**D00-T005 is structurally complete.**

Remaining quality work is operational verification of the practical labs. Once those labs are successfully executed on supported environments, their evidence status can be promoted from DRAFT to LAB-VERIFIED.
