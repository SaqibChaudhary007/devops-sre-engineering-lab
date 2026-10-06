
# D00-T002 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is the difference between user space and kernel space?
2. Why are system calls necessary?
3. A process exists but the endpoint is unavailable. What would you check next?
4. What does a sleeping process state mean conceptually?
5. Why can low CPU coexist with severe latency?
6. What is a context switch and why can excessive switching matter?
7. Why are virtual memory and memory protection important?
8. What is the relationship between a process, file descriptor and socket?
9. Why can "permission denied" be an OS-level problem rather than an application-code problem?
10. Why is "restart it" a mitigation at best, not automatically a root-cause fix?
11. What OS-level resources can a process exhaust?
12. How would you distinguish process health from service health?

## SRE

13. Which OS metrics are useful for diagnosing a latency SLO violation?
14. Why should process-up monitoring not be the only availability signal?
15. How can file-descriptor exhaustion create user-facing errors?
16. How can memory pressure affect latency before a process crashes?
17. What is the difference between host-level health and service-level health?
18. What operating-system signals might indicate saturation?
19. Why should retry behavior be considered when sockets/connections are failing?
20. When should an OS-level condition page on-call versus create a warning/ticket?

## Architect

21. When would you prefer a VM over a container for isolation reasons?
22. Why is the shared-kernel model important to container security?
23. What failure domain does a host represent?
24. How should kernel patching and host reboot requirements affect high-availability design?
25. Why can simply raising process/file limits hide an architectural problem?
26. How do connection patterns affect operating-system resource planning?
27. When do cgroup/resource controls improve multi-tenant reliability?
28. What trade-offs exist between stronger isolation and operational density?
29. Why does OS choice matter to supportability and team operations?
30. How should host limits influence capacity planning?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: failure/troubleshooting
- FD-4: reliability/operations
- FD-5: architecture/trade-offs

D00-T002 competency target: at least FD-3.
