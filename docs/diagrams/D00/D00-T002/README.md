# D00-T002 Visual / Diagram Package — Operating System Mental Model

This package provides reusable diagrams for **00.02 — Operating System Mental Model**.

## Diagram Set

1. [DIA-D00-006 — Operating System Overview](DIA-D00-006-operating-system-overview.md)
2. [DIA-D00-007 — User Space, System Calls & Kernel Boundary](DIA-D00-007-user-kernel-boundary.md)
3. [DIA-D00-008 — Process States & CPU Scheduling](DIA-D00-008-process-states-scheduling.md)
4. [DIA-D00-009 — Application I/O Through the Kernel](DIA-D00-009-application-io-kernel-flow.md)
5. [DIA-D00-010 — Virtual Machine vs Container OS Model](DIA-D00-010-vm-vs-container.md)

## Learning Progression

~~~text
What does the OS manage?
        ↓
Where is the privilege boundary?
        ↓
How does a process get CPU time?
        ↓
How does application I/O reach resources?
        ↓
How do VMs and containers differ?
~~~

## Design Rules

- one primary concept per diagram
- conceptual accuracy over excessive low-level detail
- beginner explanation before advanced interpretation
- Senior/SRE/Architect connection where useful
- Mermaid source kept editable and version-controlled

## Status

These are conceptual learning diagrams. Exact kernel internals and hardware execution paths are intentionally simplified and will be expanded in later Linux, container and networking domains.
