
---
id: D00-T001
domain: D00
title: How Computers Work
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
  required: []
  recommended: []
evidence_status:
  - RESEARCHED
  - DOC-VERIFIED
certifications: []
content_series:
  - How It Really Works
  - Under the Hood
  - Five Levels
---

# 00.01 — How Computers Work

## Start Here

Before Linux, Docker, Kubernetes, cloud, observability or SRE, you need a mental model of what a computer is actually doing.

A running application ultimately depends on a small set of fundamental resources:

~~~text
CPU
Memory
Storage
Network
I/O
~~~

This topic is not intended to turn you into a hardware engineer. It gives you the system-level foundation required to reason about performance, failures and production behavior.

## What You Will Learn

By the end of this topic, you should be able to explain:

- what CPU does
- what memory does
- what storage does
- what I/O means
- what the network does
- how a running process consumes these resources
- why applications can be slow even when CPU is low
- what a bottleneck is
- why utilization and saturation are different
- why one metric rarely proves root cause

## Prerequisites

None.

This is the first technical topic in the learning path.

---

# 1. The Core Mental Model

~~~mermaid
flowchart TB
    U[User] --> A[Application]
    A --> OS[Operating System]
    OS --> CPU[CPU]
    OS --> MEM[Memory]
    OS --> IO[I/O]
    IO --> STO[Storage]
    IO --> NET[Network]
    IO --> DEV[Devices]
~~~

Applications request work. The operating system coordinates resources. Hardware performs the work.

See the full visual package:

- [Computer System Overview](../../../docs/diagrams/D00/D00-T001/DIA-D00-001-computer-system-overview.md)
- [Memory & Storage Hierarchy](../../../docs/diagrams/D00/D00-T001/DIA-D00-002-memory-hierarchy.md)
- [Application to Hardware Flow](../../../docs/diagrams/D00/D00-T001/DIA-D00-003-application-to-hardware-flow.md)
- [Bottleneck & Queueing Model](../../../docs/diagrams/D00/D00-T001/DIA-D00-004-bottleneck-queueing.md)
- [Process & Resource Relationship](../../../docs/diagrams/D00/D00-T001/DIA-D00-005-process-resource-relationship.md)

---

# 2. CPU

The CPU executes instructions.

A simplified teaching model is:

~~~text
Fetch
→ Decode
→ Execute
→ Continue
~~~

Modern CPUs are much more complex, but this model is useful for understanding execution.

Important concepts:

- **core** — physical execution unit
- **logical CPU / hardware thread** — execution context exposed to the OS
- **register** — very small, very fast processor storage
- **cache** — fast memory close to the processor
- **clock frequency** — one characteristic of processor timing, not a complete performance measure

## CPU-Bound Work

A workload is CPU-bound when computation is the limiting factor.

Examples can include:

- compression
- encryption
- heavy calculation
- media processing
- data transformation

High CPU is not automatically bad. Ask whether the workload is meeting its latency, throughput and reliability objectives.

---

# 3. Memory

RAM is the system's active working memory.

It is generally:

- faster than persistent storage
- smaller than persistent storage
- volatile
- used by active processes, the kernel, buffers and caches

## RAM vs Storage

| RAM | Storage |
|---|---|
| Active working state | Persistent data |
| Usually volatile | Persistent |
| Faster | Slower |
| Smaller | Usually larger |

A process works with a virtual address space managed by the operating system and hardware.

Deep memory management belongs to D01 Linux Engineering.

---

# 4. Memory Hierarchy

A simplified hierarchy:

~~~text
Registers
↓
CPU Cache
↓
RAM
↓
SSD / NVMe
↓
Remote / External Storage
~~~

Moving downward generally increases capacity and latency.

This hierarchy explains why data location affects performance.

See: [DIA-D00-002 — Memory & Storage Hierarchy](../../../docs/diagrams/D00/D00-T001/DIA-D00-002-memory-hierarchy.md).

---

# 5. Storage

Storage provides persistence.

At this level, focus on four concepts:

- **capacity** — how much data can be stored
- **latency** — how long an operation takes
- **throughput** — how much data moves per unit time
- **IOPS** — I/O operations per second

Free disk space does not prove storage health.

A device may have plenty of capacity and still suffer high latency.

---

# 6. I/O

I/O means input/output: data moving between components or devices.

Examples:

- disk reads
- disk writes
- network send
- network receive
- device input

A process may spend substantial time waiting for I/O rather than actively using CPU.

This is why low CPU does not automatically mean a healthy application.

---

# 7. Network

Networking allows systems and processes to communicate.

At this level, understand:

- interface / NIC
- IP address
- port
- socket
- local vs remote communication

Simplified:

~~~text
Process
↓
Socket
↓
Operating System Networking
↓
NIC
↓
Network
↓
Remote System
~~~

Deep networking belongs to D02 Networking Mastery.

---

# 8. Program vs Process

A program exists as code/data stored on persistent storage.

A process is a running instance managed by the operating system.

~~~text
Program
→ Start
→ Process
→ CPU / Memory / Files / Network
~~~

A process has runtime state such as:

- PID
- memory
- open files
- sockets
- execution state

See: [DIA-D00-005 — Process & Resource Relationship](../../../docs/diagrams/D00/D00-T001/DIA-D00-005-process-resource-relationship.md).

---

# 9. What Happens When an Application Runs?

A simplified flow:

~~~text
Application exists on storage
        ↓
Operating system starts it
        ↓
Process is created
        ↓
Memory is allocated
        ↓
CPU executes instructions
        ↓
Process may perform storage/network I/O
        ↓
Results are returned
~~~

Containers and Kubernetes do not remove this model.

A Kubernetes pod ultimately contains processes that still depend on CPU, memory, storage and networking.

---

# 10. Bottlenecks

A bottleneck is the component limiting system performance or capacity.

Example:

~~~text
Component A: capacity 100
Component B: capacity 100
Component C: capacity 20
~~~

Overall flow may become constrained by Component C.

The bottleneck can move after an optimization.

See: [DIA-D00-004 — Bottleneck & Queueing](../../../docs/diagrams/D00/D00-T001/DIA-D00-004-bottleneck-queueing.md).

---

# 11. Utilization vs Saturation

**Utilization** asks:

> How busy is the resource?

**Saturation** asks:

> Is work waiting because the resource cannot immediately serve it?

High utilization may be healthy.

Saturation combined with increasing queues and latency is much stronger evidence of capacity pressure.

---

# 12. Latency vs Throughput

**Latency** = how long one unit of work takes.

**Throughput** = how much work completes per unit time.

A system can have:

- high throughput with poor latency
- low latency with limited throughput

Do not confuse the two.

---

# 13. Concurrency

Concurrency means multiple units of work are in progress during overlapping time periods.

More concurrency can improve throughput until another constraint appears.

Too much concurrency can create:

- contention
- queues
- context-switching overhead
- memory pressure
- downstream overload

---

# 14. Queueing Mental Model

A critical system pattern:

~~~text
Arrival Rate > Processing Rate
        ↓
Queue Grows
        ↓
Waiting Time Grows
        ↓
Latency Grows
        ↓
Timeouts / User Impact
~~~

This pattern appears in:

- web servers
- message queues
- thread pools
- database connections
- storage
- distributed systems

---

# 15. Common Beginner Mistakes

Avoid these conclusions:

### “CPU is high, therefore CPU is the root cause.”

High CPU may be expected or unrelated.

### “Free memory is low, therefore memory is broken.”

Operating systems use memory for caches and other useful purposes.

### “Disk has free space, therefore storage is healthy.”

Capacity and latency are different.

### “The NIC is UP, therefore the application is reachable.”

Many other layers can fail.

### “CPU is low, therefore the server is healthy.”

The application may be waiting on I/O or dependencies.

---

# 16. Troubleshooting Perspective

If someone says:

> “The application is slow.”

Do not begin with random commands or a restart.

Start with:

~~~text
Impact
→ Scope
→ Evidence
→ Recent Changes
→ Hypotheses
→ Test
→ Mitigation
→ Root Cause
→ Prevention
~~~

At this stage, inspect the major resource/dependency areas:

~~~text
CPU
Memory
Storage
Network
Application
Dependencies
~~~

---

# 17. Senior Engineer Perspective

A senior engineer goes beyond:

> “Which metric is high?”

and asks:

> “What is the workload doing, what is limiting it, and what is it waiting for?”

Possible answers include:

- CPU execution
- storage I/O
- network response
- database response
- lock/contention
- external dependency
- worker availability

---

# 18. SRE Perspective

An SRE connects resource conditions to user experience.

Example:

~~~text
CPU = 95%
Latency = normal
Errors = normal
Users = healthy
~~~

This may be less urgent than:

~~~text
CPU = 50%
Latency = very high
Errors = increasing
Users = affected
~~~

Resource metrics help diagnosis.

User-facing signals determine reliability impact.

---

# 19. Architect Perspective

An architect asks how resource characteristics affect design:

- should compute scale vertically or horizontally?
- is the workload stateful?
- what latency target exists?
- how much storage throughput is required?
- what network latency is acceptable?
- where are failure domains?
- what capacity headroom is required?
- what does the solution cost?

Architecture begins with requirements and constraints, not a technology name.

---

# 20. Practical Work

Complete the topic practical package:

1. [OBS-D00-001 — Observe System Resources](../../../labs/observation/D00/OBS-D00-001-observe-system-resources.md)
2. [OBS-D00-002 — Observe a Process](../../../labs/observation/D00/OBS-D00-002-observe-a-process.md)
3. [EXP-D00-001 — Resource Consumption Experiment](../../../labs/experiments/D00/EXP-D00-001-resource-consumption.md)

These labs are designed to connect abstract resource concepts to a real Linux system.

---

# 21. Assessment

Complete:

[D00-T001 Assessment Package](../../../assessments/topics/D00/D00-T001/README.md)

It includes:

- knowledge check
- applied performance scenario
- Senior/SRE/Architect follow-ups
- teach-back
- scoring rubric
- remediation guidance

---

# 22. Five-Level Explanation

## L1 — Foundation

A computer uses CPU to execute work, memory to hold active data, storage to keep persistent data and networking to communicate.

## L2 — Engineer

Applications run as processes managed by an operating system and consume CPU, memory and I/O resources.

## L3 — Senior Engineer

Performance depends on demand, contention, waiting, queueing, saturation and dependencies—not only raw utilization.

## L4 — SRE

Resource behavior matters when it affects user-facing reliability. Resource metrics are diagnostic signals; service indicators tell us whether users are suffering.

## L5 — Architect

Compute, memory, storage and network characteristics become architecture constraints involving capacity, performance, resilience, scalability and cost.

---

# 23. Teach-Back

Without notes, explain:

~~~text
Application
→ Operating System
→ CPU / Memory / I/O
→ Storage / Network
~~~

Then explain:

- one possible bottleneck
- one possible dependency
- one reason CPU could be low while latency is high
- one reason high CPU may still be healthy

If you cannot explain these clearly, revisit the topic before moving on.

---

# 24. What You Must Retain

You do not need to memorize processor engineering.

You do need to retain:

- CPU executes work.
- Memory holds active working state.
- Storage provides persistence.
- Network enables communication.
- I/O moves data.
- The operating system coordinates resources.
- Processes consume multiple resources.
- Low CPU does not prove health.
- High CPU does not prove failure.
- Bottlenecks can move.
- Symptoms and root causes may occur in different components.

---

# 25. Evidence & Sources

Core processor concepts should be verified against processor architecture documentation.

Core Linux memory concepts should be verified against Linux kernel documentation.

Repository evidence model:

- [D] Official Documentation
- [L] Lab Verified
- [P] Production Pattern
- [AI-DRAFT] AI-assisted draft pending verification

Current topic status:

- core conceptual material: RESEARCHED / DOC-VERIFIED
- practical assets: see individual lab status
- production examples: generalized learning patterns only

## Primary References

- Intel 64 and IA-32 Architectures Software Developer Manuals: https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html
- Linux Kernel Memory Management Documentation: https://www.kernel.org/doc/html/latest/mm/index.html

---

# 26. What to Learn Next

Continue to:

## 00.02 — Operating System Mental Model

The next question is:

> If applications should not directly control hardware, who manages processes, CPU time, memory, files, devices and networking?

That is the role of the operating system.
