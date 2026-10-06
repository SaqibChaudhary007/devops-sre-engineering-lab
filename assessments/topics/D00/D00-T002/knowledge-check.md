
# D00-T002 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Use short explanations, not one-word answers.

## Part A — Core Concepts

1. What are the major responsibilities of an operating system?
2. What is the kernel?
3. What is user space?
4. Why are user space and kernel space separated?
5. What is a system call?
6. Give three examples of operations that require kernel services.
7. What is a process?
8. What is a PID?
9. What does the operating-system scheduler do?
10. What is a context switch?

## Part B — Memory, Files and Devices

11. Why do applications generally use virtual memory instead of directly addressing arbitrary physical RAM?
12. What problem does memory protection solve?
13. What abstraction does a filesystem provide?
14. What is a file descriptor at a high level?
15. Why are device drivers useful?
16. How does a process usually interact with network communication?
17. What role does the kernel play in networking?
18. Why does process identity matter for security?

## Part C — Process State & Troubleshooting

19. Can a process exist but use almost no CPU? Explain.
20. Give four reasons a process may be waiting.
21. Why does "process is running" not prove that a service is healthy?
22. Why can an application be slow due to an OS-level condition even when application code has not changed?
23. What does "permission denied" suggest about where you might investigate?
24. What does "too many open files" suggest conceptually?
25. Why might a file-system problem appear as application latency?

## Part D — Containers & Architecture

26. Why do common Linux containers share the host kernel?
27. What do namespaces provide at a high level?
28. What do cgroups provide at a high level?
29. What is one key OS-level difference between a VM and a container?
30. Why does an architect need to understand operating systems?

## Self-Check

Before reviewing the rubric, ask:

- Did I explain relationships, not just definitions?
- Did I distinguish a process being alive from a service being healthy?
- Did I explain why kernel boundaries exist?
- Did I connect OS behavior to production impact?
