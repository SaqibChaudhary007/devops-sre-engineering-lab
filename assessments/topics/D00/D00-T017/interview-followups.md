# D00-T017 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is a system?
2. What is a system boundary?
3. How do you choose the right boundary?
4. What is a stock?
5. What is a flow?
6. What is a constraint?
7. What is a bottleneck?
8. Why can a bottleneck move?
9. Local vs global optimization?
10. What is a critical path?
11. What is a reinforcing feedback loop?
12. What is a balancing loop?
13. What is delay?
14. What is oscillation?
15. What is hidden coupling?
16. What is common-mode failure?
17. Why can retries amplify failure?
18. What is backpressure?

## SRE

19. How do you detect a reinforcing failure loop?
20. How do you distinguish a local saturation issue from a system bottleneck?
21. How should queue age be interpreted?
22. How do retries interact across service layers?
23. How does autoscaling delay affect stability?
24. Which signals should drive overload response?
25. How can alerting become a bad feedback loop?
26. How do humans affect incident-system behavior?
27. How do you recognize cascading failure?
28. What evidence indicates a shared failure domain?
29. How do you validate that an intervention stabilized the system?
30. Which system gaps should become reliability work?

## Architect

31. Where should the system boundary be drawn?
32. Which dependencies are too tightly coupled?
33. What should be isolated?
34. What bottleneck is likely to appear after the current one?
35. Which feedback loops are reinforcing vs balancing?
36. What delays could create instability?
37. Which metrics are system outcomes vs local indicators?
38. How should backpressure propagate?
39. Where should retry ownership live?
40. What common-mode failures defeat redundancy?
41. Which leverage point gives the best global improvement?
42. What second-order effects could follow an architecture change?
43. How should organizational incentives align with system outcomes?
44. How do you prevent architecture reviews from becoming component-by-component checklists?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: operational / troubleshooting reasoning
- FD-4: SRE / system-behavior reasoning
- FD-5: architecture / intervention / trade-off reasoning

D00-T017 competency target: at least FD-3.
