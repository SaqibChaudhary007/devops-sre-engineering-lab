
---
id: OBS-D00-001
domain: D00
topics:
  - D00-T001
level: L1
type: observation
status: draft
estimated_time: 30-45m
environment:
  - Linux VM or Linux workstation
evidence_status:
  - DRAFT
---

# OBS-D00-001 — Observe System Resources

## Objective

See CPU, memory, storage and network resources on a real system and connect them to the mental model from 00.01 — How Computers Work.

## Why This Matters

A DevOps/SRE engineer should be able to move from:

~~~text
Application
   ↓
Operating System
   ↓
CPU / Memory / Storage / Network
~~~

to a real machine and identify each resource.

## Safety

This lab is read-only. Do not change system configuration.

## Prerequisites

- D00-T001 concepts
- Access to a Linux shell

Ubuntu and RHEL-family systems can use the same commands below.

## 1. Identify the System

~~~bash
uname -a
cat /etc/os-release
~~~

Observe the operating system, kernel and architecture.

## 2. Observe CPU

~~~bash
nproc
lscpu
top
~~~

Press q to exit top.

Record:

~~~text
Logical CPUs:
Cores per socket:
Threads per core:
Load average:
Highest CPU-consuming process:
~~~

Think:
- Does the number of logical CPUs always equal physical cores?
- Is high CPU automatically an incident?
- What additional evidence would you need?

## 3. Observe Memory

~~~bash
free -h
head -20 /proc/meminfo
~~~

Record:

~~~text
Total memory:
Available memory:
Used memory:
Swap total:
Swap used:
~~~

Think:
- Why are free and available memory different?
- Does low free memory alone prove a problem?

## 4. Observe Storage

~~~bash
lsblk
df -h
~~~

Record:

~~~text
Root filesystem:
Total capacity:
Used:
Available:
Main block device:
~~~

Think:
- Does free capacity tell you storage latency?
- Can storage be slow while plenty of space remains?

## 5. Observe Network Interfaces

~~~bash
ip -brief address
ip -s link
~~~

Record:

~~~text
Primary interface:
IP address:
RX bytes/packets:
TX bytes/packets:
~~~

Think:
- Can an interface be UP while the application is unreachable?
- What else could fail?

## 6. Observe Normal Work

Open two terminals.

Terminal A:

~~~bash
top
~~~

Terminal B:

~~~bash
ls -R /usr >/dev/null 2>&1
curl -I https://example.com
~~~

If curl is unavailable, skip that command.

Observe CPU activity, processes and network counters.

## Validation Checklist

- [ ] CPU topology located
- [ ] Live CPU activity observed
- [ ] Total and available memory located
- [ ] Storage and mount points identified
- [ ] Network interfaces identified
- [ ] RX/TX counters observed
- [ ] Running processes observed

## Expected Learning Result

A running system continuously allocates CPU time, memory, storage and network resources to workloads. No single metric is enough to declare the system healthy or unhealthy.

## Troubleshooting Connection

If someone reports “the server is slow,” start with impact and scope before changing anything.

~~~text
Impact
→ Scope
→ CPU
→ Memory
→ Storage
→ Network
→ Processes
→ Recent Changes
~~~

## Interview Connection

Question: CPU is only 20%, but users report slowness. Is the server healthy?

A strong answer explains that CPU alone is insufficient. Work may be waiting on storage, network, locks, dependencies or another resource.

## Teach-Back

Without looking at the commands, explain how you would inspect the four major resources of a Linux system.

## Cleanup

No cleanup is required.

## Evidence Status

DRAFT. Promote to LAB-VERIFIED only after end-to-end execution on the stated environment.
