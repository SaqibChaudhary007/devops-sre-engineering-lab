---
id: OBS-D00-009
domain: D00
topics:
  - D00-T005
level: L2-L3
type: observation
status: draft
estimated_time: 35-50m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-009 — Detect Virtualization and Map Infrastructure Dependencies

## Objective

Determine what the operating system can reveal about virtualization and then build an evidence-based infrastructure dependency map.

## Core Rule

> Record what the system proves. Mark everything else as unknown.

Infrastructure troubleshooting becomes unreliable when engineers infer physical topology without evidence.

## Safety

This lab is read-only.

Use a personal VM/workstation or approved lab environment.

## Prerequisites

- D00-T005
- Linux shell

## 1. Detect Virtualization

If available:

~~~bash
systemd-detect-virt
~~~

Also inspect:

~~~bash
lscpu
~~~

Look for fields such as:

- Hypervisor vendor
- Virtualization type
- Virtualization flags

If available:

~~~bash
hostnamectl
~~~

Some environments may show a virtualization field.

## 2. Interpret Carefully

Possible outcomes include:

~~~text
kvm
vmware
microsoft
oracle
none
unknown
~~~

Exact output depends on the platform and tooling.

Do not conclude:

> "No virtualization detected means this is definitely bare metal."

Detection can be incomplete.

Preferred wording:

> "The available tools did not detect virtualization."

## 3. Identify Guest-Visible Resources

~~~bash
lscpu
free -h
lsblk
ip -brief addr
ip route
~~~

Record only what the guest can actually observe.

## 4. Build the Virtualization Layer Model

If virtualization is detected:

~~~text
Application
   ↓
Guest Operating System
   ↓
Virtual CPU / Memory / Disk / NIC
   ↓
Hypervisor / Virtualization Platform
   ↓
Physical Host
~~~

Mark the following as known or unknown:

~~~text
Hypervisor type:
Physical host:
Rack:
Power feed:
Physical switch:
Availability zone:
Region:
Shared storage:
~~~

Most entries may be unknown from inside the guest.

That is the point of this exercise.

## 5. Map Storage Dependency Evidence

Run:

~~~bash
lsblk -o NAME,TYPE,SIZE,FSTYPE,MOUNTPOINTS
findmnt
df -hT
~~~

Ask:

- Is the root filesystem on a block device?
- Is any mount clearly network-backed?
- Is persistence across VM deletion/replacement known?
- What cannot be established from guest inspection alone?

Do not assume a block device is physically local merely because it appears under `/dev`.

## 6. Map Network Dependency Evidence

~~~bash
ip -brief addr
ip route
ss -lnt
~~~

Build:

~~~text
Process
  ↓
Listening Socket
  ↓
Guest Network Interface
  ↓
Default Route / Gateway
  ↓
External Network
~~~

Anything below the guest-visible gateway may require platform/network documentation to prove.

## 7. Failure-Domain Exercise

Consider two VMs.

Question:

> If both VMs are running, do you know they are highly available?

Answer: not necessarily.

They could share:

- physical host
- rack
- switch
- storage
- power
- zone

Create a table:

| Layer | Evidence | Known/Unknown | Shared Failure Risk? |
|---|---|---|---|
| Guest VM | | | |
| Hypervisor | | | |
| Physical host | | | |
| Rack | | | |
| Network | | | |
| Storage | | | |
| Zone | | | |
| Region | | | |

## 8. Senior Engineer Connection

A senior engineer separates:

~~~text
Observed
vs
Inferred
vs
Unknown
~~~

This prevents incorrect root-cause claims.

## 9. SRE Connection

Reliability depends on actual failure-domain separation, not instance count alone.

## 10. Architect Connection

Redundancy decisions require knowledge of:

- placement
- shared dependencies
- capacity after failure
- failover behavior
- state availability

## Questions

1. What virtualization evidence did you find?
2. Which physical layers can the guest not prove?
3. Why can two VMs still share one failure domain?
4. Why is `/dev/sda` or `/dev/nvme...` not proof of physical-local storage?
5. What platform information would you need before claiming zone-level resilience?

## Validation Checklist

- [ ] Attempted virtualization detection
- [ ] Recorded guest-visible CPU/memory/storage/network
- [ ] Distinguished observed from inferred information
- [ ] Built a dependency map
- [ ] Marked unknown failure-domain layers explicitly
- [ ] Explained why VM count does not equal HA

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after successful execution and review.
