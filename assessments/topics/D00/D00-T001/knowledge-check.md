
# D00-T001 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Use short explanations rather than one-word responses.

## Part A — Core Concepts

1. What are the four major resource areas a running application commonly depends on?
2. What is the primary role of the CPU?
3. What is the difference between RAM and persistent storage?
4. What is a CPU core?
5. What is a logical CPU / hardware thread?
6. Why does CPU cache exist?
7. What is I/O?
8. What does storage latency mean?
9. What does throughput mean?
10. What does IOPS measure?

## Part B — Explain the Relationship

11. Explain this flow:

~~~text
Application
→ Operating System
→ CPU / Memory / Storage / Network
~~~

12. Why can an application be slow while CPU usage remains low?
13. Why does low free memory not automatically mean a memory problem?
14. Why can storage be unhealthy even when plenty of disk space is free?
15. Why can a network interface be UP while an application is still unreachable?

## Part C — Performance Reasoning

16. Define a bottleneck in your own words.
17. What is the difference between utilization and saturation?
18. What is the difference between latency and throughput?
19. Why can increasing concurrency eventually make performance worse?
20. Why is one resource metric rarely enough to declare a system healthy?

## Part D — Applied Thinking

21. CPU is 95%, but latency and errors are normal. Is there definitely an incident? Explain.
22. CPU is 20%, but latency is very high. Name at least four areas you would investigate.
23. Memory usage is increasing over time. Why should you not immediately conclude “memory leak”?
24. Database CPU is normal, but storage latency is high and application response time is poor. What hypothesis would you form?
25. A message queue grows continuously while producers are healthy. What system relationship should you compare?

## Self-Check

Before reviewing the rubric, ask yourself:

- Did I explain concepts, or only name them?
- Did I connect symptoms to possible causes?
- Did I avoid absolute statements?
