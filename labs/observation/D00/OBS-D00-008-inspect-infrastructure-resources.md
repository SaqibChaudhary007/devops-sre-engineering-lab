---
id: OBS-D00-008
domain: D00
topics:
  - D00-T005
level: L1-L2
type: observation
status: draft
estimated_time: 40-60m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-008 — Inspect Compute, Memory, Storage, and Network Resources

## Objective

Connect the infrastructure mental model to a real Linux system.

~~~text
Compute
+ Memory
+ Storage
+ Network
=
Resources available to the operating system and workloads
~~~

## Safety

This is a read-only observation lab.

Run it on a personal Linux VM/workstation or an approved lab system.

Do not run commands on production systems unless you are authorized and understand the environment.

## Prerequisites

- D00-T001
- D00-T002
- D00-T005
- Linux shell

Some commands may not exist on minimal distributions. If a command is unavailable, record that fact rather than installing tools automatically.

## 1. Identify the System

~~~bash
uname -a
hostname
~~~

If available:

~~~bash
hostnamectl
~~~

Record:

~~~text
Hostname:
Kernel:
Architecture:
Operating system:
~~~

## 2. Inspect Compute

~~~bash
lscpu
~~~

Focus on:

- Architecture
- CPU(s)
- Model name
- Core(s) per socket
- Thread(s) per core
- Virtualization indicators, if exposed

Do not assume the reported CPU count equals dedicated physical cores.

### Questions

1. How many logical CPUs are visible to the OS?
2. What CPU architecture is reported?
3. Does the output prove whether every CPU is dedicated to this system?

## 3. Inspect Memory

~~~bash
free -h
~~~

If available:

~~~bash
cat /proc/meminfo | head -20
~~~

Record:

~~~text
Total memory:
Available memory:
Used memory:
Swap:
~~~

### Important Observation

"Free" memory and "available" memory are not identical concepts on Linux.

At this level, focus on how much memory the OS can currently make available to workloads.

## 4. Inspect Block Devices

~~~bash
lsblk -o NAME,TYPE,SIZE,FSTYPE,MOUNTPOINTS
~~~

Observe:

- disks
- partitions
- logical devices
- filesystem types
- mount points

### Mental Model

~~~text
Block Device
   ↓
Partition / Logical Layer
   ↓
Filesystem
   ↓
Mount Point
   ↓
Files
~~~

Real systems may use additional layers such as LVM, RAID, encryption, network-backed devices, or cloud block volumes.

## 5. Inspect Mounted Filesystems

~~~bash
df -hT
~~~

Then:

~~~bash
findmnt
~~~

Questions:

1. Which filesystem contains `/`?
2. Which filesystem contains `/tmp`?
3. Are all mounted filesystems backed by the same underlying device?
4. Can you determine from these commands alone whether the physical storage is local or remote?

If not, say **unknown**. Do not guess.

## 6. Inspect Network Interfaces

~~~bash
ip -brief addr
~~~

Then:

~~~bash
ip link
~~~

Record:

~~~text
Interface:
IP address:
Interface state:
~~~

## 7. Inspect Routes

~~~bash
ip route
~~~

Identify:

- directly connected networks
- default route, if present
- next-hop gateway, if present

### Mental Model

~~~text
Application
   ↓
Operating System
   ↓
Network Interface
   ↓
Route Selection
   ↓
Next Hop / Destination
~~~

## 8. Inspect Listening Services

~~~bash
ss -lntup
~~~

Depending on permissions, process names may not always be visible.

Observe:

- protocol
- local address
- port
- listening state

## 9. Build the Infrastructure Snapshot

Complete:

~~~text
System
├── Architecture:
├── Logical CPUs:
├── Memory:
├── Root filesystem:
├── Root block device:
├── Network interfaces:
├── Default gateway:
└── Listening services:
~~~

## 10. Layer Connection

Explain this path using your own observed system:

~~~text
Application Process
      ↓
Operating System
      ↓
CPU / Memory
      ↓
Filesystem / Block Device
      ↓
Network Interface / Route
      ↓
Infrastructure
~~~

## Questions

1. Which resources are directly visible to the operating system?
2. Which physical details remain hidden or abstracted?
3. Why can low CPU still coexist with storage or network bottlenecks?
4. Which command showed capacity and which showed current usage?
5. What additional evidence would be needed to prove the underlying physical failure domain?

## Validation Checklist

- [ ] Identified OS/kernel/architecture
- [ ] Inspected logical CPU resources
- [ ] Inspected memory
- [ ] Inspected block devices
- [ ] Inspected filesystems/mounts
- [ ] Inspected network interfaces
- [ ] Inspected routes
- [ ] Inspected listening services
- [ ] Built a local infrastructure snapshot

## Teach-Back

Explain why:

> "The server has 8 CPUs and 16 GB RAM"

is not a complete infrastructure description.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after successful end-to-end execution on supported environments.
