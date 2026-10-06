# D00-T005 Visual / Diagram Package — Infrastructure Foundations

This package provides reusable diagrams for **00.05 — Infrastructure Foundations**.

## Diagram Set

1. [DIA-D00-023 — Physical Server Resource Model](DIA-D00-023-physical-server-resource-model.md)
2. [DIA-D00-024 — Bare Metal vs Virtual Machine](DIA-D00-024-bare-metal-vs-virtual-machine.md)
3. [DIA-D00-025 — Local vs Shared Storage](DIA-D00-025-local-vs-shared-storage.md)
4. [DIA-D00-026 — Network Path: Client → Load Balancer → Compute](DIA-D00-026-network-path-client-loadbalancer-compute.md)
5. [DIA-D00-027 — Failure Domains: Host → Rack → Zone → Region](DIA-D00-027-failure-domains.md)
6. [DIA-D00-028 — Capacity, Headroom & Failover](DIA-D00-028-capacity-headroom-failover.md)

## Learning Progression

~~~text
Physical Resources
      ↓
Virtualization
      ↓
Storage / Network Dependencies
      ↓
Failure Domains
      ↓
Capacity / Headroom
      ↓
Availability / Recovery
~~~

## Design Rules

- one primary infrastructure idea per diagram
- provider-neutral mental models
- clear physical vs virtual boundaries
- explicit dependency and failure-domain thinking
- reusable Mermaid source
- operational/SRE implications where useful
- no claim that redundancy alone equals high availability

## Status

These diagrams are conceptual. Deep virtualization, Linux, networking, storage, cloud-provider, IaC, and reliability implementation details are intentionally deferred to later domains.
