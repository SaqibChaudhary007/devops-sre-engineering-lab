
# D00-T002 Assessment Package — Operating System Mental Model

This package evaluates whether the learner can reason about the operating system as the layer that manages processes, memory, files, devices, networking, permissions and access to hardware.

## Assessment Components

1. [Knowledge Check](knowledge-check.md)
2. [Applied Scenario](applied-scenario.md)
3. [Senior / SRE / Architect Follow-Ups](interview-followups.md)
4. [Teach-Back Assessment](teach-back.md)
5. [Rubric & Remediation Guide](rubric.md)

## Recommended Order

Knowledge Check
→ Applied Scenario
→ Follow-Ups
→ Teach-Back
→ Rubric Review

## Topic Competency Guidance

Recommended minimum:

- Knowledge Check: 80%
- Applied Scenario: 75%
- Follow-Up Depth: FD-3
- Reasoning Level: at least L3
- Teach-Back: 4/5 average
- No critical misconception about kernel/user space, system calls, process state or resource management

## Critical Misconceptions

A learner should not leave this topic believing that:

- Linux is only a shell
- user-space applications directly control hardware
- a running process is always executing on CPU
- a process existing means the service is healthy
- containers normally have an independent host kernel
- the application owns CPU scheduling
- permissions are merely a file-system convenience
- low CPU proves there is no OS-level issue
