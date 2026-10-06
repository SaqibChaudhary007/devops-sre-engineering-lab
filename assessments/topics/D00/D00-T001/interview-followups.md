
# D00-T001 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. An application is slow but CPU is 15%. What does that tell you?
2. What does it mean for a process to be waiting on I/O?
3. Why can storage latency create low CPU utilization?
4. How would you distinguish CPU saturation from downstream waiting?
5. Why is “restart it” a weak first troubleshooting action?
6. What is the difference between symptom, bottleneck and root cause?
7. Why can adding more CPU fail to improve performance?
8. What happens when incoming work exceeds processing capacity?
9. Why can a queue grow even when all processes are technically running?
10. What evidence would make you confident a resource is actually the bottleneck?

## SRE

11. CPU reaches 95%, but users are healthy. Should this page on-call?
12. Which is usually closer to user experience: CPU utilization or request latency?
13. What is the role of resource metrics if they are not always paging signals?
14. How would you decide whether high resource usage is a reliability risk?
15. How does capacity headroom affect reliability?
16. When can queue growth become an SLO problem?
17. Why should alerting distinguish saturation from simple utilization?
18. What would you monitor to detect resource pressure before users are affected?

## Architect

19. Traffic will grow 10×. What should you know before adding more compute?
20. When is vertical scaling reasonable?
21. When might horizontal scaling be better?
22. Why can state make horizontal scaling harder?
23. How do storage latency and throughput requirements affect architecture?
24. How can network latency shape system design?
25. What trade-off exists between spare capacity and cost?
26. Why is “use Kubernetes” not a complete scaling answer?
27. How do downstream dependencies limit end-to-end scalability?
28. What would make you redesign rather than simply resize infrastructure?

## Follow-Up Depth Target

- FD-1: answers the root question
- FD-2: explains the concept
- FD-3: handles failure and troubleshooting
- FD-4: handles reliability implications
- FD-5: handles architecture trade-offs

For D00-T001 competency, target at least FD-3.
