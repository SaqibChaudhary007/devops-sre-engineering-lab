# D00-T006 Visual / Diagram Package — Cloud Mental Models

This package provides reusable diagrams for **00.06 — Cloud Mental Models**.

## Diagram Set

1. [DIA-D00-029 — Traditional Infrastructure vs Cloud Control Plane](DIA-D00-029-traditional-vs-cloud-control-plane.md)
2. [DIA-D00-030 — Control Plane vs Data Plane](DIA-D00-030-control-plane-vs-data-plane.md)
3. [DIA-D00-031 — IaaS vs PaaS vs SaaS Responsibility Stack](DIA-D00-031-service-model-responsibility-stack.md)
4. [DIA-D00-032 — Region / Zone / Resource Failure Domains](DIA-D00-032-region-zone-failure-domains.md)
5. [DIA-D00-033 — Elasticity & Autoscaling Loop](DIA-D00-033-elasticity-autoscaling-loop.md)
6. [DIA-D00-034 — Cloud Responsibility / Cost / Governance Triangle](DIA-D00-034-responsibility-cost-governance.md)

## Learning Progression

~~~text
Traditional Provisioning
        ↓
Cloud Control Plane / APIs
        ↓
Service Models / Responsibility
        ↓
Failure Domains
        ↓
Elasticity / Autoscaling
        ↓
Governance / Cost / Risk
~~~

## Design Rules

- provider-neutral first
- distinguish management path from workload path
- show responsibility shifts without implying it disappears
- make scaling limits and failure domains explicit
- connect architecture to reliability, governance, and cost
- keep Mermaid diagrams editable and reusable
- avoid implying cloud-native = Kubernetes

## Status

These diagrams support D00 mental models only. Provider-specific service behavior belongs later in AWS, Azure, GCP, OpenShift, IaC, SRE, and platform-engineering domains.
