---
id: D00-T010
domain: D00
title: Containers & Orchestration Mental Model
level:
  - L1
  - L2
  - L3
priority: P1
status: draft
estimated_time:
  theory: 6-8h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
    - D00-T002
    - D00-T003
    - D00-T004
    - D00-T005
    - D00-T006
    - D00-T007
    - D00-T008
    - D00-T009
  recommended: []
evidence_status:
  - RESEARCHED
certifications: []
content_series:
  - How It Really Works
  - Why Does It Exist
  - Under the Hood
  - Five Levels
  - Production Room
  - Architecture With Saqib
---

# 00.10 — Containers & Orchestration Mental Model

## Start Here

You now understand application architecture, infrastructure, cloud, DevOps, Infrastructure as Code, and CI/CD.

The next question is:

> How do we package an application so it runs consistently, and how do we operate many application instances across many machines without managing each one manually?

That is the problem space of **containers and orchestration**.

Containers are not:

- tiny virtual machines
- automatically secure
- automatically stateless
- Kubernetes by themselves
- a replacement for operating-system understanding

Orchestration is not:

- "run Docker on many servers"
- only scheduling
- only auto-scaling
- only Kubernetes

The core mental model is:

~~~text
Source
→ Image
→ Container
→ Runtime
→ Host
→ Orchestrator
→ Desired State
→ Scheduling
→ Networking
→ Storage
→ Health
→ Reconciliation
→ Observe
→ Recover
~~~

This topic stays at the mental-model level. Deep container internals, Docker/Podman, OCI, Kubernetes, OpenShift, networking, storage, scheduling, security, troubleshooting, and runtime implementation come later.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- why containers exist
- image vs container
- registry
- runtime
- container lifecycle
- process isolation at a high level
- namespaces and cgroups at a mental-model level
- filesystem layers
- writable container layer
- ephemeral vs persistent data
- container networking
- ports
- environment variables
- configuration and secrets
- volumes
- resource requests/limits at a high level
- health checks
- restart behavior
- desired replicas
- scheduling
- nodes
- control plane
- reconciliation
- service discovery
- load balancing
- rolling updates
- scaling
- stateful vs stateless workloads
- orchestration failure handling
- logs, metrics, and events
- container security boundaries
- image provenance and trust
- containers vs virtual machines
- orchestration vs CI/CD
- orchestration vs IaC
- why Kubernetes exists
- Senior/SRE/Architect reasoning

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)
- [00.02 — Operating System Mental Model](../00-02-operating-system-mental-model/README.md)
- [00.03 — Software Engineering Foundations](../00-03-software-engineering-foundations/README.md)
- [00.04 — Application Architecture Fundamentals](../00-04-application-architecture-fundamentals/README.md)
- [00.05 — Infrastructure Foundations](../00-05-infrastructure-foundations/README.md)
- [00.06 — Cloud Mental Models](../00-06-cloud-mental-models/README.md)
- [00.07 — DevOps Foundations](../00-07-devops-foundations/README.md)
- [00.08 — Infrastructure as Code Mental Model](../00-08-infrastructure-as-code-mental-model/README.md)
- [00.09 — CI/CD Mental Model](../00-09-cicd-mental-model/README.md)

You should already understand processes, operating systems, application dependencies, infrastructure, delivery pipelines, artifacts, desired state, failure domains, and production feedback.

---

# 3. Why Containers Exist

Traditional application deployment often depends heavily on the host environment.

A simplified model:

~~~text
Application
+ Runtime
+ Libraries
+ Host Configuration
→ Works Here
~~~

Move the application elsewhere:

~~~text
Different Runtime
Different Libraries
Different Configuration
→ Failure
~~~

Containers reduce this packaging uncertainty by grouping an application with much of its user-space runtime and dependencies into a portable image.

---

# 4. Container Mental Model

A container is best understood as:

> An isolated process or group of processes running on a host operating system with controlled filesystem, network, identity, and resource boundaries.

A container is **not** a complete separate physical machine.

A container normally shares the host kernel.

---

# 5. Image vs Container

An image is a packaged, read-only template.

A container is a running instance created from an image.

~~~text
Image
→ Start
→ Running Container
~~~

One image can create many containers.

~~~text
Image v1
├── Container A
├── Container B
└── Container C
~~~

---

# 6. Image as Delivery Artifact

A container image is commonly treated as a software delivery artifact.

It may contain:

- application binary/code
- runtime
- libraries
- filesystem content
- metadata
- startup definition

It should not contain unnecessary secrets or sensitive runtime credentials.

---

# 7. Registry

A registry stores and distributes container images.

~~~text
Build
→ Image
→ Registry
→ Pull
→ Runtime
~~~

A registry is to container images what an artifact repository is to other build outputs.

---

# 8. Image Identity

Tags are convenient names.

Digests identify exact content.

Conceptually:

~~~text
my-app:latest
→ mutable name

sha256:...
→ content identity
~~~

For strong traceability, production systems should know which exact image content is running.

---

# 9. Image Layers

Container images are commonly built from filesystem layers.

~~~text
Base Layer
+ Runtime Layer
+ Dependency Layer
+ Application Layer
→ Image
~~~

Layers can improve reuse and transfer efficiency.

They also create caching and supply-chain considerations.

---

# 10. Writable Container Layer

A running container typically has a writable layer above image layers.

Conceptually:

~~~text
Read-only Image Layers
+
Writable Container Layer
→ Running Filesystem View
~~~

Data written only there is tied to that container instance.

---

# 11. Ephemeral Data

If a container is removed and recreated, data stored only in its writable container layer may disappear.

Therefore:

> Container-local writable state should not be assumed to be durable.

This is one reason state placement matters.

---

# 12. Persistent Data

Persistent data should usually live outside the replaceable container lifecycle.

Examples include:

- managed databases
- persistent volumes
- object storage
- external state systems

The exact storage model depends on the platform.

---

# 13. Container Lifecycle

A simplified lifecycle is:

~~~text
Create
→ Start
→ Run
→ Stop
→ Remove
~~~

A recreated container may be a new instance even if it uses the same image.

---

# 14. Process Model

A container normally exists to run one primary workload process or tightly related process set.

If that primary process exits:

~~~text
Main Process Exits
→ Container Stops
~~~

This makes application process health important.

---

# 15. Isolation — Mental Model

Containers rely on operating-system mechanisms to isolate workloads.

At a high level:

~~~text
Namespaces
→ isolate what a process can see

cgroups
→ control / account for resource usage
~~~

Deep kernel implementation comes later.

---

# 16. Namespaces — Preview

Namespaces can isolate views of resources such as:

- processes
- networking
- mounts
- hostname
- users

The key D00 lesson:

> Containers isolate process views; they do not create a new physical machine.

---

# 17. cgroups — Preview

Control groups can organize and constrain resource consumption.

Examples:

- CPU
- memory
- process count
- I/O-related controls

The key lesson:

> Container isolation includes resource governance, not just filesystem packaging.

---

# 18. Containers vs Virtual Machines

Virtual machine:

~~~text
Hardware
→ Hypervisor
→ Guest OS Kernel
→ Applications
~~~

Container:

~~~text
Hardware
→ Host OS Kernel
→ Container Runtime
→ Isolated Application Processes
~~~

Containers usually have less per-instance OS overhead because they share the host kernel.

---

# 19. Containers Are Not "Lightweight VMs"

This phrase is convenient but incomplete.

The important difference is architectural:

> A VM virtualizes a machine boundary; a container primarily isolates processes on a shared kernel.

That difference affects security, startup, density, and troubleshooting.

---

# 20. Container Runtime

A runtime creates and manages containers on a host.

Conceptually:

~~~text
Image
→ Runtime
→ Isolated Process
~~~

The runtime interacts with the operating system to create isolation and resource boundaries.

---

# 21. Host Still Matters

Containers do not remove the host.

The host still provides:

- kernel
- CPU
- memory
- storage
- networking
- device access
- runtime

A host-level failure can affect many containers.

---

# 22. Resource Sharing

Multiple containers on one host compete for finite resources.

~~~text
Host CPU / Memory
├── Container A
├── Container B
└── Container C
~~~

Without controls, one workload can create contention for others.

---

# 23. Requests and Limits — Preview

Orchestrators may allow workloads to declare expected and maximum resources.

A mental model:

~~~text
Request
→ scheduling expectation / reservation signal

Limit
→ upper boundary
~~~

Exact semantics vary by platform and resource type.

Deep Kubernetes behavior comes later.

---

# 24. Container Networking

Containers need networking for:

- inbound traffic
- outbound traffic
- service-to-service communication
- DNS/name resolution

A container network identity may be temporary.

Therefore applications should avoid assuming one instance address is permanent.

---

# 25. Ports

Applications listen on ports inside their runtime environment.

A platform may map or expose those ports differently.

Conceptually:

~~~text
Application Port
→ Container Network
→ Service / Host / Load Balancer
→ Client
~~~

---

# 26. Configuration

Images should ideally be reusable across environments.

Environment-specific behavior can be provided through controlled configuration.

Examples:

- environment variables
- mounted configuration
- runtime parameters
- external config systems

This supports build-once/promote thinking.

---

# 27. Secrets

Secrets should be injected securely at runtime rather than baked casually into images.

Examples:

- database passwords
- API tokens
- certificates
- private keys

The exact secret mechanism is platform-specific.

---

# 28. Health Checks

A process can be running while the application is unhealthy.

Health checks answer questions such as:

~~~text
Is the process alive?
Can it receive traffic?
Has it finished starting?
~~~

Different platforms use different health-check models.

---

# 29. Restart Behavior

A stopped process can sometimes be restarted automatically.

But restart is not root-cause resolution.

~~~text
Crash
→ Restart
→ Crash
→ Restart
~~~

Repeated restart can hide persistent failure.

---

# 30. Why Orchestration Exists

One container on one host is manageable manually.

Hundreds or thousands across many hosts create new problems:

- placement
- health
- restart
- scaling
- networking
- service discovery
- rolling updates
- secrets/config
- storage
- failure recovery

Orchestration manages this system-level complexity.

---

# 31. Orchestration Mental Model

An orchestrator accepts desired workload intent and continuously manages execution toward that intent.

~~~text
Desired State
→ Scheduler / Controllers
→ Nodes
→ Running Workloads
→ Observe
→ Reconcile
~~~

---

# 32. Desired Replicas

Suppose desired state says:

~~~text
replicas = 3
~~~

Actual state:

~~~text
replicas = 2
~~~

The orchestrator attempts to restore the desired count.

This is reconciliation.

---

# 33. Reconciliation

Reconciliation repeatedly compares:

~~~text
Desired State
vs
Observed State
~~~

Then takes action.

~~~text
Desired = 3
Actual = 2
→ create replacement
~~~

This is a core orchestration mental model.

---

# 34. Controller Mental Model

Controllers watch part of system state and try to move it toward desired state.

Conceptually:

~~~text
Observe
→ Compare
→ Act
→ Observe Again
~~~

This is a control loop.

---

# 35. Node

A node is a machine that provides compute capacity for workloads.

A node may be:

- virtual machine
- physical server
- cloud instance

Many container workloads can run on one node.

---

# 36. Control Plane

The control plane manages desired state and cluster decisions.

High-level responsibilities may include:

- API
- scheduling
- controllers
- state management

The exact components vary by orchestrator.

---

# 37. Scheduler

The scheduler decides where a workload should run.

It reasons about inputs such as:

- available resources
- constraints
- placement rules
- workload requirements

Scheduling is a matching problem.

---

# 38. Placement

A workload may need particular placement because of:

- resource requirements
- hardware
- topology
- availability
- compliance
- data locality

Good placement avoids turning one failure domain into a larger outage.

---

# 39. Service Discovery

Workload instances may be created, removed, or replaced.

Clients should not depend on manually tracking individual instance addresses.

Service discovery provides a stable way to find a logical service.

---

# 40. Load Balancing

When multiple replicas serve the same workload:

~~~text
Client
→ Stable Service Endpoint
→ Replica A
→ Replica B
→ Replica C
~~~

Load balancing distributes traffic across healthy instances.

---

# 41. Scaling

Scaling can mean:

~~~text
Vertical
→ more resources per instance

Horizontal
→ more instances
~~~

Orchestration commonly supports horizontal replica changes.

But scaling the application tier can expose downstream bottlenecks.

---

# 42. Rolling Update

A rolling update replaces workload instances gradually.

Conceptually:

~~~text
v1 v1 v1
→ v2 v1 v1
→ v2 v2 v1
→ v2 v2 v2
~~~

The goal is to reduce disruption while changing versions.

---

# 43. Update Risk

A rolling update can still fail because of:

- bad image
- bad configuration
- readiness failure
- dependency incompatibility
- schema mismatch
- capacity shortage

Deployment strategy reduces risk; it does not remove risk.

---

# 44. Stateless Workload

A stateless workload does not depend on local instance-specific durable state to serve requests correctly.

This makes replacement easier.

~~~text
Instance fails
→ replace instance
→ service continues
~~~

---

# 45. Stateful Workload

A stateful workload requires durable identity/data relationships.

Examples may include:

- databases
- queues
- clustered data systems

Stateful orchestration is harder because replacement must preserve or recover data and identity assumptions.

---

# 46. Storage and Orchestration

Containers are replaceable.

Persistent storage often is not.

Therefore orchestrators must coordinate:

~~~text
Workload
↔
Persistent Storage
~~~

Storage lifecycle and workload lifecycle are related but should not be confused.

---

# 47. Failure Model

In an orchestrated environment, failures are expected.

Examples:

- container crash
- node failure
- network issue
- image pull failure
- storage issue
- unhealthy dependency
- control-plane issue
- capacity exhaustion

The system should be designed for detection and recovery.

---

# 48. Container Failure vs Node Failure

Container failure:

~~~text
One workload instance stops
~~~

Node failure:

~~~text
Many workload instances may disappear together
~~~

The blast radius is different.

---

# 49. Rescheduling

If a node fails, an orchestrator may place replacement workload instances on other healthy nodes.

This improves workload recovery.

But recovery still depends on:

- spare capacity
- storage availability
- network health
- dependencies
- control plane

---

# 50. Health vs Availability

A process can be alive but unavailable to users.

A healthy orchestrated service needs more than process existence.

Possible signals include:

- readiness
- error rate
- latency
- dependency health
- capacity

---

# 51. Logs, Metrics, and Events

Container environments generate multiple evidence types:

~~~text
Logs
→ application/runtime messages

Metrics
→ numeric behavior

Events
→ orchestration changes / failures
~~~

Troubleshooting needs correlation across these layers.

---

# 52. Ephemeral Workloads Change Troubleshooting

A failed container may disappear and be recreated quickly.

Therefore:

> Evidence must often be collected centrally rather than relying on the failed instance remaining available.

This is one reason centralized observability matters.

---

# 53. Security Boundary

Containers improve isolation but are not perfect security boundaries by themselves.

Security depends on:

- host kernel
- runtime
- permissions
- image trust
- filesystem access
- network access
- secrets
- capabilities
- orchestration policy

---

# 54. Image Trust

A secure delivery model asks:

- where did this image come from?
- who built it?
- what source produced it?
- was it scanned?
- is the exact digest known?
- is provenance available?

Image identity connects CI/CD to runtime security.

---

# 55. Least Privilege

A container should receive only the privileges it needs.

Examples of excess privilege risk:

- unnecessary root
- broad filesystem mounts
- excessive capabilities
- host access
- unrestricted network access

Deep runtime hardening comes later.

---

# 56. Orchestration and CI/CD

CI/CD typically creates and validates an artifact.

Orchestration runs and maintains workload state.

~~~text
CI/CD
→ build / test / publish image

Orchestrator
→ deploy / schedule / reconcile / recover
~~~

They are connected but not the same system.

---

# 57. Orchestration and IaC

IaC may provision:

- clusters
- networks
- node pools
- storage classes
- supporting cloud resources

Orchestration manages workload desired state inside or on top of that infrastructure.

The boundary depends on architecture.

---

# 58. Why Kubernetes Exists — Mental Model

Kubernetes is one implementation of container orchestration.

Its broad purpose is to manage desired workload state across a cluster.

At D00 level, remember:

~~~text
Declare desired workload
→ schedule
→ run
→ expose
→ monitor state
→ reconcile
→ replace / scale / update
~~~

Deep Kubernetes begins later.

---

# 59. Kubernetes Is Not the Container

A common beginner mistake is:

> "Kubernetes runs instead of containers."

More accurately:

> Kubernetes orchestrates containerized workloads through container runtime and node-level mechanisms.

The container and orchestrator are different layers.

---

# 60. Orchestration Is a Distributed System

An orchestrator coordinates many machines and many workload instances.

That introduces:

- partial failure
- network uncertainty
- stale state
- retries
- control loops
- consistency questions
- leader/control-plane concerns

This leads directly to the next topic: distributed systems.

---

# 61. Senior Engineer Perspective

A senior engineer asks:

- what image is running?
- what process is failing?
- is the problem inside the container or on the host?
- is configuration correct?
- is storage persistent?
- is the workload scheduled?
- is the service endpoint healthy?
- what changed?
- what evidence survived restart?

The goal is to find the failing layer.

---

# 62. SRE Perspective

An SRE asks:

- what is the user-visible impact?
- how many replicas are healthy?
- is the failure container-level or node-level?
- is capacity sufficient for rescheduling?
- is the orchestrator recovering automatically?
- are restarts masking a persistent problem?
- are SLOs affected?
- what is the blast radius?

---

# 63. Architect Perspective

An architect asks:

- should this workload be containerized?
- is it stateless or stateful?
- what should be externalized?
- what is the failure domain?
- what isolation is required?
- what storage model is needed?
- how should workloads be placed?
- what is the capacity model?
- how should images be trusted?
- what belongs to the platform vs application team?

---

# 64. Common Beginner Mistakes

## Mistake 1

"Container = lightweight VM."

Containers and VMs use different isolation models.

## Mistake 2

"The image is the running container."

An image is a packaged template; a container is an instance created from it.

## Mistake 3

"Data inside a container is persistent."

Container-local writable state may disappear on recreation.

## Mistake 4

"Restart means recovery."

Restart may only repeat the failure.

## Mistake 5

"Kubernetes is the container runtime."

Kubernetes is an orchestrator; runtime responsibilities are a separate layer.

## Mistake 6

"Three replicas guarantee availability."

All replicas can still depend on the same node, storage, network, or downstream system.

## Mistake 7

"Orchestration removes infrastructure problems."

Orchestrators still depend on hosts, networks, storage, identity, and capacity.

## Mistake 8

"Containers are automatically secure."

Isolation and packaging do not remove host/runtime/image/permission risks.

---

# 65. Five-Level Explanation

## L1 — Foundation

A container packages an application so it can run in an isolated environment. An orchestrator manages many containers across machines.

## L2 — Engineer

Containers combine images, runtime isolation, configuration, networking, storage, and resource controls. Orchestrators schedule, expose, restart, scale, and update workloads.

## L3 — Senior Engineer

Reliable container platforms require reasoning across image identity, runtime, host, network, storage, health, desired state, scheduling, reconciliation, and failure domains.

## L4 — SRE

Container orchestration must be evaluated through availability, replica health, capacity, recovery behavior, observability, restart loops, node failure, and SLO impact.

## L5 — Architect

Container-platform architecture balances isolation, workload characteristics, state placement, scheduling, capacity, network/storage design, image trust, platform ownership, and operational complexity.

---

# 66. What You Must Retain

Before moving on, retain:

- containers isolate processes; they are not full VMs
- containers normally share the host kernel
- image and container are different
- exact image identity matters
- registries distribute images
- image layers and writable container state are different
- container-local writable state may be ephemeral
- persistent data should survive container replacement
- the primary process lifecycle matters
- namespaces isolate views; cgroups govern resources
- hosts still matter
- resource contention still exists
- networking identity may be temporary
- configuration and secrets should be externalized deliberately
- process alive does not mean service healthy
- restart can hide persistent failure
- orchestration exists to manage many workload instances
- desired state and reconciliation are central
- schedulers place workloads onto nodes
- service discovery hides changing instance identity
- load balancing distributes traffic
- scaling can expose downstream bottlenecks
- rolling updates reduce but do not remove deployment risk
- stateless and stateful workloads have different operational needs
- node failure has a larger blast radius than container failure
- observability must survive ephemeral workload replacement
- container security depends on multiple layers
- CI/CD builds artifacts; orchestrators run/reconcile them
- IaC and orchestration manage different layers
- Kubernetes is an orchestrator, not the container itself
- orchestration is a distributed-system problem

---

# 67. Practical Package — Next Layer

The practical package should include safe, provider-neutral exercises such as:

- map image → container → runtime → host
- compare container vs VM boundaries
- model ephemeral vs persistent data
- trace container networking from process port to client
- simulate desired replicas vs actual replicas
- reason through container failure vs node failure
- design a service-discovery/load-balancing model
- classify restartable vs non-restartable failures
- reason about stateless vs stateful workload placement

These assets will be authored separately and remain DRAFT until LAB-VERIFIED.

---

# 68. Assessment Package — Pending

The assessment should test:

- why containers exist
- image vs container
- registry/runtime/host
- layers and writable state
- ephemeral vs persistent data
- namespaces/cgroups mental model
- networking and ports
- configuration/secrets
- health and restart
- desired state/reconciliation
- nodes/control plane/scheduler
- service discovery/load balancing
- scaling/update strategy
- stateless/stateful workloads
- failure and rescheduling
- observability
- security/image trust
- CI/CD + IaC + orchestration boundaries
- Senior/SRE/Architect reasoning

---

# 69. Visual Package — Pending

The visual package should include:

1. Virtual Machine vs Container
2. Image → Container → Runtime → Host
3. Image Layers + Writable Container Layer
4. Desired Replicas → Scheduler → Nodes → Reconciliation
5. Service Discovery + Load Balancing Across Replicas
6. Container Failure vs Node Failure vs Orchestrator Recovery

---

# 70. What Comes Next

After D00-T010 is completed, continue to:

## 00.11 — Distributed Systems Foundations

That topic will connect orchestration to partial failure, network uncertainty, consistency, retries, coordination, replication, and system-level trade-offs.

---

# 71. Sources & Evidence

Planned authoritative source families:

- OCI specifications
- Linux kernel documentation for namespaces/cgroups
- Docker/Podman container documentation
- Kubernetes documentation
- CNCF glossary/material
- Red Hat/OpenShift documentation where useful
- container image / registry guidance
- container and software supply-chain security guidance

Current evidence status:

- conceptual draft: RESEARCHED
- source verification: pending
- practical package: pending
- assessment package: pending
- visual package: pending
