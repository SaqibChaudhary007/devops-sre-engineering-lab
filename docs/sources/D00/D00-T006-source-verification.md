# D00-T006 Source Verification — Cloud Mental Models

## Verification Goal

Verify the core factual claims in **00.06 — Cloud Mental Models** against standards and official cloud architecture, reliability, autoscaling, quota, shared-responsibility, and cloud-native guidance.

## Verification Status

**Result:** Core claims verified.

**Evidence level:** E2 — supported by standards, official provider documentation, and authoritative cloud-native references.

This topic remains intentionally provider-neutral. Provider-specific behavior belongs in later AWS/Azure/GCP/OpenShift domains.

## Verified Claim Map

| Topic claim | Verification | Source |
|---|---|---|
| Cloud includes on-demand self-service, broad network access, resource pooling, rapid elasticity, and measured service | Verified | NIST SP 800-145 |
| IaaS, PaaS, and SaaS are standard cloud service-model categories | Verified | NIST SP 800-145 |
| Public, private, community, and hybrid are NIST deployment-model categories | Verified | NIST SP 800-145 |
| Control plane handles administrative/resource-management operations while the data plane delivers the primary service function | Verified | AWS Fault Isolation Boundaries |
| Autoscaling can change capacity based on schedules, thresholds, and metrics | Verified | Microsoft Azure VM Scale Sets autoscale documentation |
| Availability zones are intended as more isolated infrastructure groups inside supported regions | Verified | Azure Well-Architected / Reliability guidance |
| Region/zone support and topology vary by provider/service | Verified | Azure reliability documentation |
| Security/compliance responsibility is shared and changes depending on the service consumed | Verified | AWS Shared Responsibility Model |
| Cloud services enforce quotas/service limits | Verified | AWS Service Quotas documentation |
| Cloud-native is broader than Kubernetes and emphasizes dynamic environments, resilient/manageable/observable systems, declarative APIs, immutable infrastructure, and automation | Verified | CNCF Cloud Native Definition |

## Primary / Authoritative Sources

### NIST SP 800-145 — Definition of Cloud Computing

- https://csrc.nist.gov/pubs/sp/800/145/final
- https://www.nist.gov/publications/nist-definition-cloud-computing

Supports:

- on-demand self-service
- broad network access
- resource pooling
- rapid elasticity
- measured service
- IaaS
- PaaS
- SaaS
- deployment models

Important nuance:

> NIST's formal deployment models include public, private, community, and hybrid cloud.

"Multi-cloud" is widely used industry terminology but is not one of the four NIST SP 800-145 deployment-model categories.

### AWS — Control Planes and Data Planes

- https://docs.aws.amazon.com/whitepapers/latest/aws-fault-isolation-boundaries/control-planes-and-data-planes.html

Supports:

- control plane as administrative/resource-management APIs
- data plane as the primary service/workload function
- distinction between configuration/orchestration and workload/data operations
- different failure characteristics between management and workload paths

Important nuance:

> The exact control-plane/data-plane split varies by service. Do not assume every provider or product draws the boundary identically.

### Microsoft Azure — Autoscale

- https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview

Supports:

- manual scale changes
- schedule-based autoscaling
- metric-threshold autoscaling
- dynamically increasing/decreasing VM instance count

Important nuance:

> Autoscaling only changes the capacity it controls. It does not prove that the scaled tier is the actual bottleneck.

### Microsoft Azure — Regions and Availability Zones

- https://learn.microsoft.com/en-us/azure/well-architected/design-guides/regions-availability-zones
- https://learn.microsoft.com/azure/reliability/availability-zones-region-support

Supports:

- regions as geographic infrastructure boundaries
- availability zones as more isolated groups of datacenters within supported regions
- independent power/cooling/networking characteristics in Azure
- zonal, zone-redundant, and multi-region design trade-offs
- differences in service/region zone support

Important nuance:

> Region and zone semantics, service availability, topology, and guarantees are provider-specific.

### AWS — Shared Responsibility Model

- https://aws.amazon.com/compliance/shared-responsibility-model/
- https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/shared-responsibility.html

Supports:

- provider/customer security responsibility split
- provider operation of underlying cloud infrastructure
- customer responsibility for workload configuration, data, identities, applications, and guest OS in relevant service models
- responsibilities varying according to the services chosen

Important nuance:

> "Managed" does not mean "provider handles everything." Responsibility shifts as the abstraction level changes.

### AWS — Service Quotas

- https://docs.aws.amazon.com/servicequotas/
- https://docs.aws.amazon.com/servicequotas/latest/userguide/reference_limits.html

Supports:

- quotas/limits exist
- quotas can cap resource counts and API usage
- limits can be account-, service-, or region-scoped depending on the service

Important nuance:

> "Cloud has unlimited capacity" is false. Workloads must account for quotas, provider capacity, service constraints, and regional availability.

### CNCF — Cloud Native Definition

- https://www.cncf.io/wp-content/uploads/2020/08/CNCF-Webinar-_-Delivering-Cloud-Native-Application-and-Infrastructure-Management.pdf
- https://www.cncf.io/blog/2021/05/05/announcing-the-cloud-native-glossary/

Supports the broader cloud-native mental model:

- scalable applications in modern dynamic environments
- public/private/hybrid cloud contexts
- containers, service meshes, microservices, immutable infrastructure, and declarative APIs as examples
- resilient, manageable, observable systems
- robust automation
- frequent, predictable change with reduced toil

Important nuance:

> Cloud-native is not synonymous with Kubernetes. Kubernetes is one implementation technology within a larger operating and architectural model.

## Verified Nuances / Corrections

### 1. Cloud Is More Than Remote Hosting

The NIST model explicitly includes on-demand self-service, rapid elasticity, measured service, broad network access, and resource pooling.

Therefore:

> "Cloud is someone else's computer" is an incomplete mental model.

### 2. Scalability and Elasticity Are Related but Different

Scalability is the ability to support increased demand.

Elasticity emphasizes dynamically matching allocated capacity to changing demand.

### 3. Control Plane and Data Plane Can Fail Differently

A management/API problem does not always mean already-running workload traffic is unavailable, and vice versa.

Troubleshooting should distinguish:

~~~text
Can I manage the resource?
vs
Can the resource perform its workload function?
~~~

### 4. Managed Services Shift Responsibility

They do not eliminate customer responsibility.

The exact split depends on:

- service model
- provider
- configuration
- integration
- data
- identity
- legal/compliance requirements

### 5. Multi-Cloud Is Not a NIST Deployment Model

The topic can teach multi-cloud as an industry architecture/operating pattern, but it should not present it as one of NIST's formal deployment models.

### 6. Public Cloud Does Not Mean Publicly Reachable

"Public" refers to the cloud deployment/service model, not whether every workload endpoint is internet-accessible.

### 7. Serverless Still Uses Servers

The server lifecycle and infrastructure management are abstracted further from the customer.

### 8. Autoscaling Is Not Automatic Performance Repair

Autoscaling is effective only when:

- the chosen signal represents useful demand
- the resource can scale quickly enough
- downstream dependencies can absorb the added load
- state and architecture support the scaling model

### 9. Zones Are Not Universal DR

Multi-zone architecture improves resilience against some localized failure classes, but disaster recovery is a broader recovery strategy involving scope, data, recovery time, recovery point, and often separate locations.

### 10. Cloud Capacity Is Not Infinite

Quotas, service limits, regional capacity, API limits, and product constraints are real architectural considerations.

### 11. Cloud-Native Is Not Kubernetes

Kubernetes may support cloud-native practices, but cloud-native also includes automation, observability, resilience, declarative systems, immutable infrastructure, and dynamic environments.

### 12. Faster Provisioning Increases Governance Importance

API-driven infrastructure allows fast creation and change.

That makes:

- least privilege
- policy
- review
- logging
- quotas
- cost controls
- blast-radius management

more important, not less.

## Evidence Decision

The following D00-T006 areas are now eligible for **DOC-VERIFIED** status:

- cloud essential characteristics
- IaaS/PaaS/SaaS mental model
- public/private/hybrid cloud mental models
- control plane vs data plane
- API-driven/on-demand provisioning
- elasticity
- autoscaling
- region/zone failure-domain framing
- managed-service/shared-responsibility framing
- quotas/service limits
- cloud-native framing

## Still Conceptual / Provider-Neutral

The following remain valid D00 mental models but should not be interpreted as identical provider implementations:

- region topology
- zone topology
- autoscaling signals/features
- identity object types
- tagging models
- serverless runtime behavior
- managed-service responsibility boundaries
- quota scopes

These are explored later in provider-specific domains.

## Not Yet LAB-VERIFIED

Source verification is not practical verification.

The following still require controlled exercises:

- map control-plane vs data-plane actions
- classify service models and responsibility boundaries
- classify ephemeral vs persistent resources
- reason through a two-zone failure scenario
- model autoscaling decisions without creating paid resources
- design a tagging/ownership/governance model
- identify quota and blast-radius risks in a hypothetical environment

Those become the D00-T006 practical package.
