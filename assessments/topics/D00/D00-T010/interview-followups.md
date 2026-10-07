# D00-T010 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Why do containers exist?
2. Image vs container: what is the operational difference?
3. Why is an image digest stronger than a mutable tag?
4. How do image layers and writable container state differ?
5. Why is container-local state usually a poor place for durable data?
6. Why is a container not a lightweight VM?
7. What does the runtime own?
8. What does the host still own?
9. What do namespaces isolate?
10. What do cgroups govern?
11. Why can resource requests/limits be misunderstood?
12. What is the difference between startup, liveness, and readiness?
13. Why can restart loops hide root cause?
14. What is desired state?
15. What is reconciliation?
16. What does the scheduler actually decide?
17. What makes a workload unschedulable?
18. Why does service discovery matter?

## SRE

19. How does container failure differ from node failure?
20. Why does replica count not guarantee availability?
21. How does spare capacity affect recovery?
22. What evidence should survive workload replacement?
23. How would you diagnose repeated restarts?
24. How would you diagnose a readiness-only failure?
25. Why do deployment and runtime signals need correlation?
26. How does node saturation affect scheduling?
27. How can network/path-specific failure reduce ready capacity?
28. What should happen when new rollout replicas fail readiness?
29. What makes self-healing bounded?
30. How do stateful workloads change recovery objectives?

## Architect

31. When should a workload be containerized?
32. When is containerization unnecessary complexity?
33. What state should be externalized?
34. How should image trust be enforced conceptually?
35. How should workloads be spread across failure domains?
36. How much spare capacity should be reserved for recovery?
37. How should service identity be separated from instance identity?
38. How should persistent storage lifecycle be designed?
39. What changes for stateful workloads?
40. Where should health responsibility live?
41. How should logs/metrics/events be centralized?
42. Which responsibilities belong to app teams vs platform teams?
43. How should CI/CD, IaC, and orchestration boundaries interact?
44. Why is Kubernetes an orchestration layer rather than the container runtime?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / runtime reasoning
- FD-4: reliability / recovery reasoning
- FD-5: architecture / platform trade-offs

D00-T010 competency target: at least FD-3.
