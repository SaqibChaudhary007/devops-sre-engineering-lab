# D00-T005 — Teach-Back Assessment

## Goal

Demonstrate that you can explain infrastructure from beginner level through architecture decisions without hiding behind cloud-provider product names.

## Task A — Beginner

Explain:

- physical server
- virtual machine
- CPU
- memory
- storage
- network

Use one simple analogy.

## Task B — Engineer

Explain this stack:

~~~text
Application
→ Operating System
→ Virtual CPU / Memory / Disk / NIC
→ Hypervisor
→ Physical Host
~~~

Then explain what changes when the workload runs on bare metal.

## Task C — Senior Engineer

Explain why this statement is wrong:

> "We have two VMs, so we are highly available."

Include:

- host
- rack
- storage
- network
- zone
- capacity after failure

## Task D — SRE

Explain the difference between:

~~~text
Capacity
Utilization
Saturation
Headroom
~~~

Then explain how low CPU can coexist with poor service performance.

## Task E — Architect

Compare infrastructure choices across:

~~~text
Bare Metal
vs
Virtual Machines
vs
Managed Cloud Infrastructure
~~~

Discuss:

- performance
- provisioning
- failure domains
- operational burden
- security responsibility
- cost
- scaling
- recovery

## Storage Challenge

Explain the difference between:

~~~text
Block
File
Object
~~~

without naming a vendor product.

## Failure-Domain Diagram Challenge

Draw from memory:

~~~text
Application
↓
VM
↓
Host
↓
Rack
↓
Zone
↓
Region
~~~

Then add:

- one shared storage dependency
- one network dependency
- one SPOF
- one redundancy improvement
- one capacity/headroom consideration

## Scoring

Score 1–5 for:

- correctness
- clarity
- infrastructure-layer reasoning
- failure-domain reasoning
- capacity reasoning
- SRE connection
- architecture trade-off awareness

Target: average 4/5 with no critical misconception.
