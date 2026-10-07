# D00-T010 Source Verification — Containers & Orchestration Mental Model

## Verification Goal

Verify the core claims in **00.10 — Containers & Orchestration Mental Model** against current OCI specifications, Linux kernel documentation, Docker documentation, and Kubernetes documentation.

## Verification Status

**Result:** Core claims verified with important implementation-specific nuances around container identity, runtime boundaries, resource controls, persistence, health, scheduling, reconciliation, and self-healing.

**Evidence level:** E2 — supported by open standards, Linux kernel documentation, and official container/orchestration platform documentation.

This topic remains at the D00 mental-model level. Deep OCI internals, Docker/Podman, Linux namespaces/cgroups, Kubernetes, OpenShift, scheduling, networking, storage, security, and troubleshooting belong to later domains.

---

## Verified Claim Map

| Topic claim | Verification | Primary source |
|---|---|---|
| A container image packages application content plus runtime dependencies | Verified | Kubernetes Containers; Docker Images |
| OCI standardizes image/runtime/distribution formats rather than one vendor implementation | Verified | OCI overview/specifications |
| Images are composed of filesystem layers | Verified | OCI Image Spec; Docker image-layer docs |
| Exact image content can be identified by digest | Verified | OCI descriptor/image manifest; Kubernetes Images |
| A container is a running isolated process created from an image | Verified | Docker Containers; Kubernetes Containers |
| Containers usually share the host kernel rather than booting a guest kernel | Verified as the common Linux-container model | Docker/Kubernetes model + Linux isolation primitives |
| cgroups organize processes and control resource distribution | Verified | Linux kernel cgroup v2 docs |
| Container-local writable state should not be treated as durable | Verified | Docker layered-filesystem model; Kubernetes storage model |
| PersistentVolume lifecycle is independent of an individual Pod | Verified | Kubernetes Persistent Volumes |
| Kubernetes control loops move current state toward desired state | Verified | Kubernetes Controllers |
| The scheduler assigns unscheduled Pods to Nodes based on resources and constraints | Verified | Kubernetes Cluster Architecture |
| Kubernetes Services provide stable service abstraction over changing Pods | Verified | Kubernetes Services/Networking |
| Readiness, liveness, and startup checks represent different health questions | Verified | Kubernetes Probes |
| Kubernetes can replace failed workload replicas and reschedule after node failure | Verified with capacity/storage caveats | Kubernetes Self-Healing |
| Rolling updates gradually replace old replicas with new ones | Verified | Kubernetes Deployments |
| Stateful workloads require stronger identity/storage handling than interchangeable stateless replicas | Verified | Kubernetes StatefulSets |
| Kubernetes is an orchestrator for containerized workloads, not the container runtime itself | Verified | Kubernetes Overview / Containers |
| Orchestration depends on control plane, nodes, runtime, networking, storage, and capacity | Verified | Kubernetes Cluster Architecture |

---

# Primary / Authoritative Sources

## 1. Open Container Initiative — Container Standards

- https://opencontainers.org/
- https://opencontainers.org/about/overview/
- https://specs.opencontainers.org/image-spec/manifest/
- https://specs.opencontainers.org/image-spec/config/
- https://specs.opencontainers.org/image-spec/descriptor/
- https://specs.opencontainers.org/runtime-spec/runtime/?v=v1.3.0

Supports:

- OCI as an open standards body for image, runtime, and distribution specifications
- image manifests and configurations
- filesystem layers
- content-addressable descriptors/digests
- separation between OCI image representation and runtime execution

### Important nuance

> "Container" is an implementation concept built from several layers.

OCI standardizes interfaces and formats; it does not mean every container engine has identical internal architecture.

---

## 2. Docker Documentation — Containers, Images, Layers

- https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-container/
- https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/
- https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/

Supports:

- containers as isolated processes
- images as standardized packages
- immutable image layers
- container-specific writable filesystem layer
- multiple containers created from the same image

### Important nuance

A container's writable layer is tied to that container instance.

Therefore:

> Writing data inside a container does not automatically make the data durable.

Durability depends on an external/persistent storage mechanism.

---

## 3. Linux Kernel — cgroup v2

- https://docs.kernel.org/admin-guide/cgroup-v2.html

Supports:

- cgroup as a mechanism to organize processes hierarchically
- controlled distribution/accounting of system resources
- the mental model that resource governance is separate from filesystem packaging

### Important nuance

The D00 topic should keep cgroups at a conceptual level.

Exact CPU/memory enforcement semantics, throttling, OOM behavior, hierarchy rules, and controller details belong to later Linux/container/Kubernetes sections.

---

## 4. Kubernetes — Containers and Images

- https://kubernetes.io/docs/concepts/containers/
- https://kubernetes.io/docs/concepts/containers/images/

Supports:

- container images as ready-to-run software packages
- containers decoupling applications from host infrastructure
- container runtimes managing container execution/lifecycle
- registries as image distribution points
- image tags vs immutable digests
- Kubernetes using CRI-compatible container runtimes

### Important nuance

Tags are names that can move.

Digests identify exact image content.

For production traceability:

> "Which tag?" is weaker evidence than "Which digest/content identity?"

---

## 5. Kubernetes — Cluster Architecture, Nodes, Scheduling

- https://kubernetes.io/docs/concepts/architecture/
- https://kubernetes.io/docs/concepts/architecture/nodes/

Supports:

- control plane + worker node architecture
- nodes running Pods
- scheduler selecting Nodes for unscheduled Pods
- scheduling decisions based on resource requirements and constraints
- kubelet/runtime responsibility on nodes
- node capacity and allocatable-resource concepts

### Important nuance

A scheduler does not make capacity appear.

If the cluster lacks suitable capacity, workloads can remain unscheduled.

---

## 6. Kubernetes — Controllers and Reconciliation

- https://kubernetes.io/docs/concepts/architecture/controller/

Supports:

- control loops
- desired state vs current state
- controllers repeatedly acting to move current state toward desired state
- multiple specialized controllers rather than one monolithic loop

### Important nuance

Reconciliation is continuous control-loop behavior.

It does not mean the system instantly reaches desired state or that all failures can be healed automatically.

---

## 7. Kubernetes — Health Probes

- https://kubernetes.io/docs/concepts/workloads/pods/probes/

Supports distinct health questions:

- startup: has the application finished starting?
- liveness: should the container be restarted?
- readiness: should the workload receive traffic?

### Important nuance

These are not interchangeable.

A process can be alive while not ready to serve traffic.

Incorrect probe design can create its own outages.

---

## 8. Kubernetes — Networking / Service Abstraction

- https://kubernetes.io/docs/concepts/services-networking/

Supports:

- Pods having network identities
- service/network abstractions over changing workload instances
- communication across Pods and Nodes
- stable logical service access despite workload replacement

### Important nuance

Individual workload addresses should not be treated as permanent application identities.

Service discovery exists because workload instances are replaceable.

---

## 9. Kubernetes — Storage and Persistent Volumes

- https://kubernetes.io/docs/concepts/storage/
- https://kubernetes.io/docs/concepts/storage/persistent-volumes/

Supports:

- temporary and long-term storage as different concerns
- PersistentVolume lifecycle independent of an individual Pod
- separation between compute/workload lifecycle and durable storage lifecycle

### Important nuance

> "Container is replaceable" does not mean "data is replaceable."

Stateful systems require storage, identity, backup, recovery, and consistency reasoning beyond simple replica replacement.

---

## 10. Kubernetes — Workloads, Deployments, StatefulSets

- https://kubernetes.io/docs/concepts/workloads/controllers/
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/

Supports:

- higher-level workload APIs managing Pods declaratively
- replacement of failed Pods
- rolling updates
- Deployments as a good fit for interchangeable/stateless replicas
- StatefulSets for stable identity, persistent storage, and ordered behavior

### Important nuance

Stateless vs stateful is not about whether an application ever touches data.

It is about whether an individual workload instance depends on durable instance-specific state/identity to function correctly.

---

## 11. Kubernetes — Self-Healing

- https://kubernetes.io/docs/concepts/architecture/self-healing/

Supports:

- container restart based on policy
- replica replacement
- rescheduling/recovery after some node failures
- Service endpoint updates around failed workloads
- persistent-volume recovery in supported scenarios

### Important nuance

"Self-healing" does not mean root-cause resolution.

Kubernetes can restart or replace workload instances, but it cannot automatically fix every application bug, bad configuration, unavailable dependency, storage failure, quota problem, or exhausted cluster.

---

# Verified Nuances / Corrections

## 1. Container = Process Isolation, Not a Tiny VM

For mainstream Linux containers, the important model is:

~~~text
Shared Host Kernel
+ Isolated Process View
+ Resource Controls
+ Packaged User Space
~~~

A VM normally has its own guest kernel.

This difference matters for security, troubleshooting, density, startup behavior, and host dependency.

## 2. Image and Container Are Different Lifecycle Objects

~~~text
Image
→ immutable packaged content

Container
→ runtime instance created from that image
~~~

One image can create many independent container instances.

## 3. Image Tags Are Not Strong Content Identity

Tags can be moved.

Digests identify content.

Therefore production traceability should prefer immutable content identity where possible.

## 4. Writable Container State Is Ephemeral by Default

Image layers remain unchanged.

A running container may write to its own writable layer.

If the container is removed, that writable state should not be assumed to survive.

## 5. Persistence Is a Separate Lifecycle

Persistent storage should survive individual workload replacement when the application requires durability.

Kubernetes PersistentVolumes explicitly model storage lifecycle independently from an individual Pod.

## 6. Resource Requests and Limits Must Stay a Preview at D00

Kubernetes scheduling considers requested resources.

Limit behavior is resource-specific and deeper than the D00 mental model.

Therefore D00 should not overgeneralize requests as guaranteed runtime reservation or limits as identical enforcement for every resource.

## 7. Health Questions Are Different

~~~text
Startup
→ has initialization completed?

Liveness
→ should this container be restarted?

Readiness
→ should traffic be sent here?
~~~

"Process running" is not the same as "service ready."

## 8. Restart Is Not Root-Cause Recovery

Restart can recover transient process failure.

A repeated crash/restart loop can also be evidence of a persistent application/config/dependency problem.

## 9. Reconciliation Is Not Instantaneous

Controllers continuously compare desired and current state.

Recovery still depends on:

- control-plane health
- node capacity
- image availability
- networking
- storage
- dependencies
- policy/permissions

## 10. Scheduling Is a Constraint/Capacity Decision

Schedulers select suitable nodes.

They do not create application correctness or unlimited capacity.

Unschedulable workloads are a valid failure mode.

## 11. Replica Count Alone Does Not Prove Availability

Multiple replicas can still share:

- one node/failure domain
- one storage dependency
- one network path
- one database
- one external service

Availability requires failure-domain reasoning.

## 12. Service Discovery Exists Because Instances Change

Individual container/Pod addresses may change as workloads are recreated.

Applications should target stable service abstractions rather than manually track instance addresses.

## 13. Stateful Workloads Need More Than Replica Replacement

Stateful systems may require:

- stable identity
- durable storage
- ordered operations
- quorum/replication awareness
- backup/restore
- data consistency

This is why stateful orchestration is more complex.

## 14. Kubernetes Is Not the Runtime

Kubernetes orchestrates workloads.

Node-level runtimes such as containerd or CRI-O execute containers through Kubernetes' runtime integration.

Therefore:

~~~text
Kubernetes
≠
Container Runtime
~~~

## 15. Self-Healing Has Boundaries

Kubernetes can restart, replace, and reschedule workloads in many cases.

It cannot automatically repair every underlying bug or dependency failure.

"Self-healing" should be taught as **automated state restoration within defined platform capabilities**, not unlimited automatic recovery.

---

# Evidence Decision

The following D00-T010 areas are now eligible for **DOC-VERIFIED** status:

- image vs container
- image registries / image identity
- layers and writable container state
- container runtime mental model
- cgroup resource-governance mental model
- container vs VM boundary
- ephemeral vs persistent storage
- node/control-plane architecture
- scheduling
- desired state / reconciliation
- probes and health distinctions
- service-discovery / networking abstraction
- rolling update mental model
- stateless vs stateful workload distinction
- workload replacement / self-healing caveats
- Kubernetes vs container-runtime distinction

---

# Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require structured exercises:

- map image → container → runtime → host
- compare VM and container boundaries
- model image layers + writable state
- classify ephemeral vs persistent data
- trace application port → container network → service/client
- model desired replicas vs observed replicas
- reason through container failure vs node failure
- classify startup/liveness/readiness health questions
- model scheduler/resource constraints
- design service-discovery/load-balancing flow
- compare stateless vs stateful recovery
- correlate logs/metrics/events across container, node, and orchestrator layers

These become the D00-T010 practical package.
