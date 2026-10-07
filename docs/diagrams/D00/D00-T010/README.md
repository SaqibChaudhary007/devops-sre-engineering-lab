# D00-T010 Visual / Diagram Package — Containers & Orchestration Mental Model

This package provides reusable diagrams for **00.10 — Containers & Orchestration Mental Model**.

## Diagram Set

1. [DIA-D00-053 — Virtual Machine vs Container](DIA-D00-053-vm-vs-container.md)
2. [DIA-D00-054 — Image → Container → Runtime → Host](DIA-D00-054-image-container-runtime-host.md)
3. [DIA-D00-055 — Image Layers + Writable Container Layer](DIA-D00-055-image-layers-writable-layer.md)
4. [DIA-D00-056 — Desired Replicas → Scheduler → Nodes → Reconciliation](DIA-D00-056-replicas-scheduler-nodes-reconciliation.md)
5. [DIA-D00-057 — Service Discovery + Load Balancing Across Replicas](DIA-D00-057-service-discovery-load-balancing.md)
6. [DIA-D00-058 — Container Failure vs Node Failure vs Orchestrator Recovery](DIA-D00-058-container-node-orchestrator-recovery.md)

## Learning Progression

~~~text
Package
→ Run
→ Isolate
→ Persist
→ Schedule
→ Discover
→ Balance
→ Reconcile
→ Recover
~~~

## Design Rules

- stay provider-neutral
- distinguish image, container, runtime, host, and orchestrator
- show that mainstream Linux containers share the host kernel
- separate image layers from writable runtime state
- distinguish workload lifecycle from storage lifecycle
- show desired state vs observed state explicitly
- make scheduler/capacity constraints visible
- show service identity separately from instance identity
- make node-level blast radius larger than single-container failure
- represent self-healing as bounded recovery, not magic
- keep Mermaid diagrams editable and reusable

## Status

These diagrams support D00 mental models only. Deep OCI internals, Docker/Podman, Linux namespaces/cgroups, Kubernetes/OpenShift scheduling, networking, storage, security, and troubleshooting belong to later domains.
