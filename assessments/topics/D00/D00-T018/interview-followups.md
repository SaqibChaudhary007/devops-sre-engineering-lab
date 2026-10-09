# D00-T018 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Fault vs error vs failure?
2. What is a failure mode?
3. Why can slow behavior be a failure?
4. What is partial failure?
5. What is a failure domain?
6. What is blast radius?
7. What is common-mode failure?
8. Why can redundancy fail?
9. What is retry amplification?
10. Why are timeout budgets important?
11. What is graceful degradation?
12. What is load shedding?
13. What is backpressure?
14. What is state uncertainty?
15. Why can failover fail?
16. Why is backup not recovery?

## SRE

17. How do you distinguish transient from persistent failure?
18. How do retries affect overloaded dependencies?
19. When should you shed load?
20. How do you validate graceful degradation?
21. How do you detect gray/observer-dependent failure?
22. What evidence shows a cascading failure?
23. How do you validate recovery end-to-end?
24. What is the role of restore testing?
25. How do RTO/RPO affect operational readiness?
26. How should a game day be designed?
27. What stop conditions should failure testing have?
28. How do you prevent alerting from hiding user impact?
29. What does a failed runbook reveal?
30. Which resilience gaps should become reliability work?

## Architect

31. How do you design failure domains?
32. Which dependencies should be isolated?
33. What common-mode dependencies defeat redundancy?
34. Which capabilities may degrade safely?
35. Where should retry ownership live?
36. Where should timeout boundaries be enforced?
37. What state must survive failover?
38. Which recovery objective drives topology?
39. How do you validate a secondary is actually ready?
40. What failure modes should a circuit breaker address?
41. What must remain protocol-specific in partition/quorum design?
42. How do you design recovery validation?
43. How do you balance prevention cost with tolerated failure risk?
44. What evidence would justify a production chaos experiment?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: operational / troubleshooting reasoning
- FD-4: SRE / resilience reasoning
- FD-5: architecture / recovery / trade-off reasoning

D00-T018 competency target: at least FD-3.
