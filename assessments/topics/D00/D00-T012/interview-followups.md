# D00-T012 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Reliability vs availability: what is the difference?
2. Why can a healthy component still participate in an unreliable user journey?
3. What is a critical user journey?
4. What is a failure model?
5. What is a failure domain?
6. What is blast radius?
7. Why does redundancy need independence?
8. What is graceful degradation?
9. What makes failover trustworthy?
10. Why is a backup not recovery?
11. What is the difference between RTO and RPO?
12. What does MTTR mean in your organization?
13. Why should that definition be explicit?
14. What is capacity headroom?
15. Why can a node failure trigger cascading saturation?
16. Rollback vs roll-forward: when do you choose each?
17. What makes an alert actionable?
18. What does production readiness require?

## SRE

19. How do you choose an SLI for checkout?
20. How do SLOs influence operational priorities?
21. What does an error budget represent?
22. What should happen when error-budget consumption is unhealthy?
23. Why is 100% reliability usually a poor target?
24. How would you measure time to detect?
25. How would you measure time to respond?
26. How would you measure time to recover?
27. Why can averages hide severe recovery events?
28. How does retry traffic affect failover headroom?
29. How can graceful degradation protect an SLO?
30. How can alert design reduce MTTR?

## Architect

31. What reliability target does this workload actually need?
32. Which failures must be tolerated?
33. Which failure domains must be independent?
34. How much spare capacity is justified?
35. When is active/active appropriate?
36. When is active/passive appropriate?
37. Which dependencies can degrade?
38. What RTO/RPO are justified?
39. How should backup and restore be validated?
40. How should change safety be designed?
41. How much redundancy is enough?
42. When is added reliability complexity not worth the cost?
43. What operational ownership model supports recovery?
44. How should reliability be reviewed before production launch?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / recovery reasoning
- FD-4: SRE / operational reliability reasoning
- FD-5: architecture / business trade-off reasoning

D00-T012 competency target: at least FD-3.
