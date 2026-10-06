
---
id: D00-T002
domain: D00
title: Operating System Mental Model
level:
  - L1
  - L2
  - L3
priority: P1
status: published
estimated_time:
  theory: 4-6h
  practical: 1-2h
  assessment: 1-2h
prerequisites:
  required:
    - D00-T001
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications:
  - RHCSA
  - LFCS
  - K8S-PREREQ
content_series:
  - How It Really Works
  - Under the Hood
  - Five Levels
---

# 00.02 — Operating System Mental Model

## Start Here

In 00.01, you learned that applications ultimately depend on CPU, memory, storage, network and I/O.

Now ask the next question:

> If applications should not directly control hardware, who manages access to those resources?

That is one of the core jobs of the **operating system**.

This topic builds the mental model you will need before Linux, containers, Kubernetes, OpenShift, performance troubleshooting and production operations.

---

# 1. What You Will Learn

By the end of this topic, you should be able to explain:

- what an operating system is responsible for
- kernel space vs user space
- why applications use system calls
- how processes are created and managed
- how CPU scheduling fits into application execution
- how memory is managed at a high level
- how filesystems provide storage abstractions
- how device drivers connect software to hardware
- how networking is exposed to applications
- how privilege boundaries improve isolation and security
- why containers share a host kernel
- why OS knowledge matters in DevOps/SRE troubleshooting

---

# 2. Prerequisites

Required:

- [00.01 — How Computers Work](../00-01-how-computers-work/README.md)

You should already understand:

- CPU
- RAM
- storage
- network
- I/O
- process as a running program
- bottleneck
- utilization vs saturation

---

# Learning Package Navigation

Use this topic as the canonical learning page. Move through the package in this order:

1. **Learn** — complete the conceptual sections on this page.
2. **Visualize** — review the [D00-T002 visual package](../../../../docs/diagrams/D00/D00-T002/README.md).
3. **Observe** — complete [OBS-D00-003 — Observe the Operating System Boundary](../../../../labs/observation/D00/OBS-D00-003-observe-os-boundary.md).
4. **Trace** — complete [OBS-D00-004 — Observe System Calls](../../../../labs/observation/D00/OBS-D00-004-observe-system-calls.md).
5. **Experiment** — complete [EXP-D00-002 — Process States, Scheduling and Waiting](../../../../labs/experiments/D00/EXP-D00-002-process-states-scheduling-waiting.md).
6. **Assess** — complete the [D00-T002 Assessment Package](../../../../assessments/topics/D00/D00-T002/README.md).
7. **Teach Back** — explain the topic at Beginner, Engineer, Senior, SRE and Architect levels.
8. **Continue** — move to 00.03 only when the core mental model is clear.

## Visual Package

The dedicated diagrams are:

- [DIA-D00-006 — Operating System Overview](../../../../docs/diagrams/D00/D00-T002/DIA-D00-006-operating-system-overview.md)
- [DIA-D00-007 — User Space, System Calls & Kernel Boundary](../../../../docs/diagrams/D00/D00-T002/DIA-D00-007-user-kernel-boundary.md)
- [DIA-D00-008 — Process States & CPU Scheduling](../../../../docs/diagrams/D00/D00-T002/DIA-D00-008-process-states-scheduling.md)
- [DIA-D00-009 — Application I/O Through the Kernel](../../../../docs/diagrams/D00/D00-T002/DIA-D00-009-application-io-kernel-flow.md)
- [DIA-D00-010 — Virtual Machine vs Container OS Model](../../../../docs/diagrams/D00/D00-T002/DIA-D00-010-vm-vs-container.md)

## Practical Package

- [OBS-D00-003 — Observe the Operating System Boundary](../../../../labs/observation/D00/OBS-D00-003-observe-os-boundary.md)
- [OBS-D00-004 — Observe System Calls](../../../../labs/observation/D00/OBS-D00-004-observe-system-calls.md)
- [EXP-D00-002 — Process States, Scheduling and Waiting](../../../../labs/experiments/D00/EXP-D00-002-process-states-scheduling-waiting.md)

The practical assets remain **DRAFT** until they are executed end-to-end and promoted to `LAB-VERIFIED`.

## Assessment Package

The [D00-T002 Assessment Package](../../../../assessments/topics/D00/D00-T002/README.md) includes:

- 30-question knowledge check
- applied OS/resource scenario
- Senior/SRE/Architect follow-ups
- teach-back assessment
- scoring rubric
- remediation map

---

# 3. The Core Operating System Mental Model

A useful first model:

~~~mermaid
flowchart TB
    U[User] --> APP[Application / User Process]
    APP --> SYS[System Call Interface]
    SYS --> K[Kernel]

    K --> CPU[CPU Scheduling]
    K --> MEM[Memory Management]
    K --> FS[Filesystem]
    K --> NET[Networking]
    K --> DEV[Device Drivers]
    K --> SEC[Security / Permissions]

    DEV --> HW[Hardware]
    CPU --> HW
    MEM --> HW
    FS --> HW
    NET --> HW
~~~

The operating system provides:

- abstraction
- resource management
- isolation
- controlled access to hardware
- common services for applications

A program does not need to know how every disk controller, network card or CPU model works.

The OS provides consistent interfaces.

---

# 4. What Is an Operating System?

An operating system is the software layer that manages hardware resources and provides services/abstractions to applications.

At this level, think of it as responsible for:

~~~text
CPU scheduling
Memory management
Process management
Filesystem management
Device management
Networking
Security / permissions
Resource accounting
System interfaces
~~~

Linux is an operating-system kernel commonly used together with user-space tools and libraries to form a complete Linux operating system environment.

---

# 5. Kernel vs User Space

One of the most important concepts in systems engineering is the separation between:

~~~text
User Space
and
Kernel Space
~~~

## User Space

Most applications run in user space.

Examples:

- web servers
- databases
- shells
- Python programs
- monitoring agents
- container runtimes and helpers

Applications in user space have restricted direct access to privileged hardware operations.

## Kernel Space

The kernel operates with elevated privilege and manages core system resources.

It handles areas such as:

- process scheduling
- memory management
- networking
- filesystems
- devices
- security enforcement

---

# 6. Why This Separation Exists

Imagine every application could directly:

- overwrite arbitrary memory
- control disks
- reconfigure network hardware
- access every process
- modify kernel state

One application bug could destroy system stability or expose every other workload.

The separation provides controlled boundaries.

~~~text
Application
    ↓
Controlled Interface
    ↓
Kernel
    ↓
Hardware
~~~

This is fundamental to security and stability.

---

# 7. System Calls

Applications still need privileged services.

For example, an application may need to:

- open a file
- create a process
- allocate/manage memory
- send network data
- read from a device

It requests these through the operating-system interface, commonly via **system calls**.

Conceptually:

~~~text
Application
   ↓
Library / Runtime
   ↓
System Call
   ↓
Kernel
   ↓
Resource / Device
~~~

Examples of system-call concepts on Linux include operations such as:

- read
- write
- open/openat
- close
- fork/clone
- execve
- socket
- connect
- mmap

You do not need to memorize them yet.

---

# 8. Why System Calls Matter to DevOps/SRE

Many production problems eventually involve what a process is asking the kernel to do.

Examples:

~~~text
Application waiting on file read
Application waiting on socket
Application cannot open more files
Application blocked on memory allocation
Application receives permission denied
Process cannot bind to port
~~~

Later tools such as `strace` help observe system-call behavior.

That belongs in D01 Linux Engineering.

---

# 9. Process Management

The OS creates, tracks and manages processes.

A process has attributes such as:

- PID
- parent relationship
- execution state
- memory mappings
- open files
- credentials
- resource usage

Conceptually:

~~~text
Executable
   ↓
OS loads/starts
   ↓
Process
   ↓
Scheduled onto CPU
~~~

---

# 10. Process States — Mental Model

A process is not always actively executing.

A simplified model:

~~~text
Ready
  ↓
Running
  ↓
Waiting / Sleeping
  ↓
Ready again
~~~

A process may wait for:

- disk I/O
- network response
- timer
- lock
- another process/event

This explains why:

> A running application can be slow even when it is not consuming much CPU.

---

# 11. CPU Scheduling

Multiple processes want CPU time.

The operating system scheduler decides which runnable work gets CPU time.

Conceptually:

~~~text
Process A ─┐
Process B ─┼─→ Scheduler → CPU
Process C ─┘
~~~

The scheduler must balance:

- fairness
- responsiveness
- throughput
- priorities
- available cores

Deep scheduling internals belong to D01.

---

# 12. Context Switching

When CPU execution moves from one process/thread to another, the system must preserve and restore execution state.

Conceptually:

~~~text
Run A
 ↓
Save A state
 ↓
Load B state
 ↓
Run B
~~~

This is called a **context switch**.

Context switching is necessary, but excessive switching can add overhead.

This becomes relevant later in performance engineering.

---

# 13. Memory Management

The operating system helps manage:

- physical memory
- virtual address spaces
- page allocation
- memory protection
- reclaim
- caching
- swap
- out-of-memory situations

Applications generally operate in virtual address spaces rather than directly manipulating arbitrary physical RAM.

Conceptually:

~~~text
Process A Virtual Memory ─┐
                          ├─→ Kernel + MMU → Physical Memory
Process B Virtual Memory ─┘
~~~

This supports abstraction and isolation.

---

# 14. Memory Protection

Processes should not normally be able to freely read or overwrite another process's memory.

The OS and processor memory-management mechanisms enforce boundaries.

This matters for:

- security
- reliability
- fault isolation

A bug in Process A should not automatically corrupt Process B.

---

# 15. Filesystem Abstraction

Applications generally work with files and directories rather than raw disk sectors.

~~~text
Application
   ↓
File API
   ↓
Filesystem
   ↓
Block I/O
   ↓
Storage Device
~~~

The filesystem provides abstractions such as:

- files
- directories
- paths
- metadata
- permissions
- ownership

Deep filesystem study belongs to D01.

---

# 16. File Descriptors — Preview

On Unix-like systems, processes interact with many resources through integer handles called file descriptors.

These can represent:

- files
- sockets
- pipes
- devices

This leads to an important Unix/Linux mental model:

> Many I/O resources can be accessed through file-like interfaces.

You will study file descriptors deeply later.

---

# 17. Device Management

Applications should not need custom low-level logic for every hardware device.

The operating system uses device drivers to communicate with hardware.

~~~text
Application
   ↓
Kernel Interface
   ↓
Driver
   ↓
Device
~~~

Examples:

- storage controller
- NIC
- GPU
- USB device

---

# 18. Networking Role of the OS

Applications usually use sockets.

The OS handles networking functions such as:

- protocol implementation
- sockets
- packet transmission/reception
- routing decisions
- interface management
- port allocation
- firewall integration

Simplified:

~~~text
Application
   ↓
Socket
   ↓
Kernel Network Stack
   ↓
NIC
   ↓
Network
~~~

Deep networking belongs to D02.

---

# 19. Privilege and Security

Not every process should have the same permissions.

The OS helps enforce:

- users
- groups
- file permissions
- process credentials
- privileged operations
- access controls

At a high level:

~~~text
Normal User Process
        ↓
Restricted Operations

Privileged Context
        ↓
More Sensitive Operations
~~~

This reduces blast radius.

---

# 20. User Mode vs Kernel Mode

Modern processors support privilege levels that allow the OS kernel to execute privileged operations while ordinary applications run with restricted privileges.

Conceptually:

~~~text
User Mode
   ↓ system call / controlled transition
Kernel Mode
   ↓
Hardware operation
~~~

This is a hardware-supported security boundary, not merely a naming convention.

---

# 21. Interrupts and Events

Hardware and software events must sometimes notify the system.

Examples:

- network packet arrives
- disk operation completes
- timer fires
- exception occurs

The kernel handles these events and coordinates further processing.

Do not memorize low-level interrupt architecture yet.

Understand the purpose:

> The system needs efficient ways to react to events without constantly polling everything.

---

# 22. Boot — High-Level Preview

Before applications can run, the machine must initialize hardware and start the operating system.

A simplified Linux-style flow:

~~~text
Firmware
  ↓
Bootloader
  ↓
Kernel
  ↓
Early userspace / initramfs
  ↓
Init system
  ↓
Services
  ↓
Applications
~~~

Deep Linux boot architecture belongs to D01.

---

# 23. Services and Daemons

Servers often run long-lived background processes called services or daemons.

Examples:

- web server
- SSH server
- monitoring agent
- database

On modern Linux systems, these are often managed by systemd.

At this level:

~~~text
OS boots
  ↓
Service manager starts services
  ↓
Processes remain running
  ↓
Users/applications consume service
~~~

---

# 24. Resource Management

The OS must manage finite resources.

Examples:

- CPU time
- memory
- open files
- processes
- network sockets
- devices

Resource limits exist because unlimited access by one workload can harm others.

This becomes very important later with:

- Linux resource limits
- cgroups
- containers
- Kubernetes requests/limits

---

# 25. Why Containers Depend on the OS

A container is not a tiny virtual machine with its own independent hardware kernel by default.

Linux containers rely heavily on host-kernel features.

Conceptually:

~~~text
Container A ─┐
Container B ─┼─→ Host Linux Kernel → Hardware
Container C ─┘
~~~

Containers can have isolated views of resources, but they share the host kernel.

This is why understanding the OS becomes a prerequisite for understanding containers and Kubernetes properly.

---

# 26. Container Isolation Preview

Linux containers use kernel mechanisms such as:

- namespaces
- cgroups
- capabilities
- filesystem isolation mechanisms

At this stage, only retain:

~~~text
Namespaces → isolation / different views
cgroups → resource control/accounting
Capabilities → split privileged powers
~~~

Deep container internals belong to D05.

---

# 27. Virtual Machine vs Container — OS Perspective

Simplified:

## Virtual Machine

~~~text
Application
↓
Guest OS / Kernel
↓
Virtual Hardware
↓
Hypervisor
↓
Physical Hardware
~~~

## Container

~~~text
Application
↓
Container Isolation
↓
Shared Host Kernel
↓
Physical / Virtual Hardware
~~~

This distinction is foundational.

---

# 28. What Happens When a Web Request Arrives?

Suppose a Linux web server receives a request.

Conceptually:

~~~text
Network packet arrives
       ↓
Kernel networking handles packet
       ↓
Socket data becomes available
       ↓
Application process wakes/runs
       ↓
Scheduler gives CPU time
       ↓
Application may read memory/files
       ↓
Application writes response
       ↓
Kernel networking sends response
~~~

The OS participates throughout the request lifecycle.

---

# 29. Why Application Problems Can Actually Be OS Problems

A service can fail because of:

- process not running
- permission denied
- port unavailable
- filesystem full
- file-descriptor exhaustion
- memory pressure
- CPU starvation
- storage I/O delay
- network-stack issue
- kernel/resource limits

So:

> “The application is broken”

does not necessarily mean:

> “The application code is wrong.”

---

# 30. Why OS Problems Can Look Like Application Problems

Example:

~~~text
Disk latency increases
        ↓
Application file/database operations wait
        ↓
Worker threads remain occupied
        ↓
Queue grows
        ↓
Request latency increases
~~~

Users see:

> Slow application.

The underlying problem may be OS/storage behavior.

---

# 31. Senior Engineer Troubleshooting View

When a Linux-hosted application is unhealthy, a senior engineer may ask:

~~~text
Is the process running?
What state is it in?
Is CPU available?
Is there memory pressure?
Is storage slow/full?
Are file descriptors exhausted?
Is networking healthy?
Are permissions blocking access?
Did configuration change?
What is the process waiting for?
~~~

The key question again:

> What is the workload doing, and what is it waiting for?

---

# 32. SRE Perspective

The SRE connects OS behavior to service reliability.

Example:

~~~text
Host memory pressure
        ↓
Application slows
        ↓
Request latency rises
        ↓
SLO begins burning
~~~

OS telemetry helps explain the failure.

Service-level indicators determine user impact.

Useful categories later include:

- CPU saturation
- memory pressure
- disk latency
- filesystem capacity
- network errors
- process health
- resource exhaustion

---

# 33. Architect Perspective

An architect should understand the OS because design choices depend on operating characteristics.

Questions include:

- should workloads share a host?
- what isolation is required?
- VM or container?
- what resource limits are needed?
- what kernel capabilities are required?
- what failure domain does a host represent?
- how will patching/reboots affect availability?
- which OS family supports the workload?
- what operational skills does the team have?

Architecture is not independent of operating-system behavior.

---

# 34. Common Beginner Mistakes

## Mistake 1

“Linux is just a command line.”

Linux is an operating-system kernel and ecosystem, not simply a shell.

## Mistake 2

“Application accesses disk directly.”

Usually the application interacts through OS/filesystem interfaces.

## Mistake 3

“If a process exists, the service is healthy.”

A process may exist but be stuck, blocked, unhealthy or unreachable.

## Mistake 4

“Containers have their own full kernel.”

Typical Linux containers share the host kernel.

## Mistake 5

“CPU is controlled by the application.”

The OS scheduler controls how runnable work receives CPU time.

---

# 35. Five-Level Explanation

## L1 — Foundation

The OS manages hardware and provides common services to applications.

## L2 — Engineer

Applications run in user space and request privileged operations through controlled kernel interfaces such as system calls.

## L3 — Senior Engineer

Application behavior depends on process state, scheduling, memory, filesystems, I/O, networking, permissions and resource limits.

## L4 — SRE

OS metrics and kernel/resource behavior help explain service reliability problems, but user-facing SLI/SLO impact determines operational priority.

## L5 — Architect

OS choice, isolation model, kernel dependency, resource control, failure domain, patching and operational skill all influence system design.

---

# 36. What You Must Retain

Before moving on, retain these ideas:

- the OS manages finite hardware resources
- kernel space and user space are different privilege domains
- applications request kernel services through controlled interfaces
- processes are scheduled onto CPU
- processes can be running, ready or waiting
- virtual memory provides abstraction/isolation
- filesystems abstract storage
- sockets expose networking to applications
- drivers connect the kernel to hardware
- process existence does not equal service health
- containers share the host kernel in the common Linux container model
- OS behavior can directly affect application reliability

---

# 37. Completion Gate & What Comes Next

Before moving on, confirm that you can:

- explain kernel space vs user space
- explain why system calls exist
- distinguish process existence from service health
- explain why processes can wait without using much CPU
- describe the OS role in memory, filesystems, networking and devices
- explain why common Linux containers share the host kernel
- complete the practical package
- score at least 80% on the knowledge check
- demonstrate at least L3 / FD-3 reasoning in the assessment
- teach the mental model clearly without relying on notes

Then continue to:

## 00.03 — Software Engineering Foundations

That topic will explain:

- source code
- compilation vs interpretation
- dependencies
- build process
- artifacts
- runtime
- how software becomes something the operating system can execute

---

# 38. Sources & Evidence

Primary references for the mental model:

- Linux kernel documentation: https://docs.kernel.org/
- Linux kernel memory management documentation: https://docs.kernel.org/mm/
- Linux namespaces documentation: https://man7.org/linux/man-pages/man7/namespaces.7.html
- Linux cgroups documentation: https://docs.kernel.org/admin-guide/cgroup-v2.html
- Linux system calls overview: https://man7.org/linux/man-pages/man2/syscalls.2.html
- Linux capabilities overview: https://man7.org/linux/man-pages/man7/capabilities.7.html

Status:

- conceptual material: RESEARCHED / DOC-VERIFIED
- practical package: authored as DRAFT; LAB-VERIFICATION pending
- assessment package: authored and cross-linked
- visual package: authored and cross-linked
- canonical learner journey: integrated

## Topic Package Status

**D00-T002 is structurally complete.**

Remaining quality work is operational verification of the practical labs. Once those labs are executed successfully on supported environments, their evidence status can be promoted from DRAFT to LAB-VERIFIED.
