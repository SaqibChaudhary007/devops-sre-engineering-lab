
# D00-T002 — Rubric & Remediation Guide

Use this after attempting the assessment.

## Knowledge Check — Expected Concepts

Strong answers should demonstrate:

- OS as resource manager and abstraction layer
- kernel/user-space privilege separation
- system calls as controlled interfaces
- processes as OS-managed execution contexts
- scheduler as CPU-time allocator
- processes can wait/sleep without consuming CPU
- virtual memory and protection provide abstraction/isolation
- filesystems abstract persistent storage
- file descriptors represent process I/O handles
- sockets expose network communication
- identities and permissions enforce access control
- common Linux containers share the host kernel
- namespaces isolate views; cgroups control/account resources

## Knowledge Score

- 90–100%: strong
- 80–89%: competent
- 70–79%: review recommended
- below 70%: revisit D00-T002

Critical misconception override: no competency if the learner believes process existence guarantees service health, containers always have independent kernels, or user processes directly control privileged hardware.

## Applied Scenario — 100 Points

| Dimension | Points |
|---|---:|
| Impact & scope | 10 |
| Process/OS mental model | 15 |
| Hypothesis quality | 15 |
| Evidence selection | 15 |
| File-descriptor/socket reasoning | 15 |
| Safe troubleshooting approach | 10 |
| SRE reasoning | 10 |
| Architecture/trade-offs | 10 |

Pass: 75/100.

Strong: 85+/100.

## Strong Scenario Reasoning

A strong response should consider file-descriptor/socket exhaustion as a leading hypothesis without assuming it is proven.

Useful evidence can include:

- per-process open descriptor count
- configured process limits
- host-wide descriptor pressure
- socket states
- connection-pool behavior
- dependency reachability
- system logs
- process state

It should avoid immediately raising limits without understanding why descriptors/connections are accumulating.

## Follow-Up Evaluation

- L1: defines OS/kernel/process concepts
- L2: connects user space to kernel services
- L3: troubleshoots resource/waiting conditions
- L4: connects OS behavior to SLO and incident impact
- L5: evaluates isolation/resource/failure-domain trade-offs

Topic competency target: L3 / FD-3 minimum.

## Teach-Back Evaluation

Score 1–5:

1. major gaps
2. partial understanding
3. mostly correct
4. clear and accurate
5. adaptable, production-aware and trade-off aware

Target: 4/5 average.

## Remediation Map

If weak on:

- kernel vs user space → revisit sections 3–6
- system calls → revisit sections 7–8 and OBS-D00-004
- process states → revisit sections 9–12 and EXP-D00-002
- memory protection → revisit sections 13–14
- files/files descriptors → revisit sections 15–16
- networking role → revisit section 18
- security/permissions → revisit sections 19–20 and OBS-D00-003
- containers/shared kernel → revisit sections 25–27
- production reasoning → revisit sections 29–33
