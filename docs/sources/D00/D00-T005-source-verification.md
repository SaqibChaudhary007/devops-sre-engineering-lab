# D00-T005 Source Verification — Infrastructure Foundations

## Verification Goal

Verify the core factual claims in **00.05 — Infrastructure Foundations** against official infrastructure, virtualization, storage, networking, cloud reliability, infrastructure-as-code, and shared-responsibility documentation.

## Verification Status

**Result:** Core claims verified.

**Evidence level:** E2 — documented by primary/official or authoritative technical sources.

The topic intentionally teaches portable infrastructure mental models. Provider-specific implementation details remain deferred to later AWS, Azure, Linux, networking, storage, and IaC domains.

## Verified Claim Map

| Topic claim | Verification | Source |
|---|---|---|
| Virtualization hosts can run multiple guest virtual machines using a hypervisor | Verified | Red Hat virtualization documentation |
| Host failure can affect multiple guest VMs sharing that host | Verified by virtualization model | Red Hat virtualization documentation |
| Local/instance storage can be tied to compute lifecycle | Verified | AWS EC2 instance-store documentation |
| Block storage presents attachable block devices/volumes | Verified | AWS EBS documentation |
| File storage exposes shared filesystem-oriented access | Verified | AWS EC2/EFS documentation |
| Object storage is accessed as objects rather than as ordinary block devices | Verified | AWS EC2/S3 documentation |
| Routing tables determine how traffic reaches destination networks | Verified | Linux ip-route documentation |
| Availability zones/regions are used to isolate failure and improve resilience | Verified | Microsoft Azure Well-Architected guidance |
| Redundancy across failure domains improves resilience but increases cost/complexity | Verified | Microsoft Azure Architecture Center |
| IaC manages infrastructure through versionable configuration rather than only manual UI operations | Verified | HashiCorp Terraform documentation |
| Shared responsibility differs between provider and customer and varies by service model | Verified | AWS shared-responsibility documentation |

## Primary / Authoritative Sources

### Red Hat Virtualization / KVM

- https://docs.redhat.com/en/documentation/red_hat_virtualization/4.2/html/administration_guide/chap-hosts
- https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/virtualization_deployment_and_administration_guide/index

Supports:

- virtualization host / hypervisor model
- guest virtual machines
- KVM-based virtualization
- multiple VMs on physical infrastructure

Important nuance:

> "Bare metal" can be used in different ways across the industry.

In this topic, **bare-metal workload** means a general-purpose operating system/workload running directly on physical hardware rather than inside a VM. Some hypervisors themselves also run directly on physical hardware, so "bare metal" should not be treated as meaning "hypervisors cannot exist."

### AWS EC2 Storage

- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Storage.html
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html
- https://docs.aws.amazon.com/ebs/latest/userguide/

Supports:

- instance/local storage tied to instance lifecycle
- block storage volumes
- differences between temporary instance storage and persistent EBS-style block storage
- file/object storage categories around EC2 workloads

### AWS File and Object Storage

- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/file-storage.html

Supports the high-level distinction that file storage provides shared filesystem access, while object storage is accessed through an object-storage service/API model.

Important nuance:

> Object-storage products can sometimes be exposed through gateways, FUSE layers, or compatibility tools, but object storage is not natively the same abstraction as a POSIX filesystem or block device.

### Linux Routing

- https://man7.org/linux/man-pages/man8/ip-route.8.html

Supports the routing mental model used in the topic: systems use routing tables and route selection to determine how packets reach destination networks.

### Azure Availability Zones and Regions

- https://learn.microsoft.com/en-us/azure/architecture/high-availability/building-solutions-for-high-availability
- https://learn.microsoft.com/en-us/azure/architecture/aws-professional/regions-zones

Supports:

- regions as larger geographic infrastructure groupings
- availability zones as more isolated datacenter groups within supported regions
- independent power/cooling/networking for zones
- using redundancy across zones/regions for resilience
- cost/complexity trade-offs of greater redundancy

Important nuance:

> Exact meanings, guarantees, topology, and service support differ across cloud providers.

The topic therefore keeps region/zone definitions deliberately provider-neutral.

### Terraform / Infrastructure as Code

- https://developer.hashicorp.com/terraform/tutorials/aws-get-started/infrastructure-as-code

Supports:

- managing infrastructure through configuration files
- versioning infrastructure definitions
- review/collaboration
- consistent/repeatable changes
- automation of infrastructure lifecycle

Important nuance:

> IaC does not automatically eliminate drift, errors, or unsafe changes. Quality still depends on review, state handling, testing, access control, and operational discipline.

### AWS Shared Responsibility Model

- https://aws.amazon.com/compliance/shared-responsibility-model/
- https://docs.aws.amazon.com/prescriptive-guidance/latest/addf-security-and-operations/shared-responsibility-model.html

Supports:

- provider/customer responsibility boundaries
- provider responsibility for underlying cloud infrastructure
- customer responsibility for workload/data/configuration responsibilities depending on service
- responsibility boundaries varying by service model

## Verified Nuances / Corrections

### 1. vCPU Is a Scheduling/Virtualization Abstraction

Do not teach:

> 1 vCPU always equals 1 dedicated physical core.

The mapping depends on platform, hypervisor, CPU topology, allocation model, and scheduling.

### 2. Local Storage Lifetime Is Platform-Specific

Local/instance storage may be physically attached or closely coupled to a compute host, but exact persistence guarantees differ by platform.

The portable lesson is:

> Understand whether storage survives instance replacement, stop/start, host failure, or rescheduling.

### 3. "Block vs File vs Object" Are Access Models

Do not reduce the difference to product names.

Think in terms of the interface presented:

- block device
- filesystem/files/directories
- object/key + metadata API

### 4. Failure Domains Must Be Real, Not Cosmetic

Two VMs are not strongly redundant if they share the same host, rack, power source, storage dependency, or zone.

### 5. Availability Zone Definitions Are Provider-Specific

Do not assume AWS, Azure, and GCP use identical topology or service guarantees.

### 6. Redundancy Is Not the Same as High Availability

Redundancy helps only when:

- components are healthy
- traffic can fail over
- state remains accessible
- capacity remains sufficient
- shared dependencies do not fail together

### 7. Utilization Is Not Saturation

A low CPU percentage does not prove infrastructure health.

Queues, storage latency, network limits, memory pressure, connection limits, IOPS, and dependency waits can still constrain the workload.

### 8. Immutable Infrastructure Is a Pattern

Replacing instances rather than mutating them can reduce drift and improve traceability, but it is not universally required for every system.

### 9. IaC Improves Repeatability, Not Automatic Correctness

IaC makes infrastructure definitions reviewable and repeatable, but a wrong configuration can be reproduced consistently too.

### 10. Shared Responsibility Changes by Service

The customer/provider boundary is different for:

- virtual machines
- managed databases
- serverless
- SaaS

Never apply one responsibility diagram blindly to every service.

## Evidence Decision

The following D00-T005 areas are now eligible for **DOC-VERIFIED** status:

- virtualization host/guest mental model
- hypervisor concept
- vCPU abstraction
- local vs persistent/shared storage concepts
- block/file/object storage mental model
- routing foundation
- failure-domain concept
- zone/region resilience mental model
- redundancy and HA trade-off framing
- Infrastructure as Code foundation
- cloud shared-responsibility preview

## Not Yet LAB-VERIFIED

Documentation verification is not laboratory verification.

The following still require controlled hands-on execution:

- inspect CPU, memory, storage, and network interfaces on Linux
- detect virtualization indicators
- inspect block devices and mounted filesystems
- inspect IP addresses and routes
- inspect listening services
- observe safe resource headroom/saturation behavior
- draw the real local infrastructure dependency path

Those become the D00-T005 practical package.
