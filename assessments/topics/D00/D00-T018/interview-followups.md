# D00-T018 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Fault vs error vs failure?
2. What is a failure mode?
3. What is blast radius?
4. What is a failure domain?
5. Transient vs permanent failure?
6. Partial vs intermittent failure?
7. Why can slow behavior be failure?
8. What is gray/observer-dependent failure?
9. What is common-mode failure?
10. Why can redundancy still fail together?
11. What is failure propagation?
12. What is cascading failure?
13. Why can retries amplify incidents?
14. What is fail-fast behavior?
15. What is graceful degradation?
16. What is backpressure?
17. What is load shedding?
18. Why is a circuit breaker not always appropriate?

## SRE

19. How do you identify retry amplification in production?
20. How do you distinguish dependency slowness from caller saturation?
21. What signals indicate overload?
22. When should you shed load?
23. What evidence confirms graceful degradation is working?
24. How do you validate containment?
25. How do you know recovery is real?
26. Why can alerting extend an incident?
27. How do you validate a runbook?
28. How do you test failover assumptions safely?
29. How do RTO/RPO influence operational readiness?
30. What failure assumptions should become game-day scenarios?

## Architect

31. How do you identify the real failure domains?
32. Which dependencies must be independent?
33. Where should isolation boundaries exist?
34. Which dependencies should degrade vs fail closed?
35. Where should retry ownership live?
36. How should timeout budgets compose?
37. Which workloads can be load-shed?
38. What common-mode risks defeat multi-region design?
39. How do recovery objectives shape architecture?
40. What evidence proves backups are usable?
41. How should state uncertainty be handled?
42. Which partition/quorum claims can be made generically, and which are protocol-specific?
43. What should be tested before launch?
44. How do you constrain chaos/failure experiments?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: operational / troubleshooting reasoning
- FD-4: SRE / resilience reasoning
- FD-5: architecture / recovery / trade-off reasoning

D00-T018 competency target: at least FD-3.
