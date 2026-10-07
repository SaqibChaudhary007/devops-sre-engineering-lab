# D00-T014 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is observability?
2. How is observability different from monitoring?
3. What is telemetry?
4. What is instrumentation?
5. Why are metrics/logs/traces/events complementary?
6. What is context?
7. What is correlation?
8. Request ID vs trace ID: what is the difference?
9. What is a span?
10. Why does structured logging matter?
11. What is metric cardinality?
12. Why are request IDs dangerous metric labels?
13. Why can averages hide latency problems?
14. What does p95 mean?
15. What is black-box monitoring?
16. What is white-box monitoring?
17. Why are change markers useful?
18. Why does correlation not prove causation?

## SRE

19. Which user-centered signals should page?
20. How should observability support an SLO?
21. How would you detect missing telemetry during incidents?
22. How do RED and USE guide investigation?
23. How do dependency signals reduce MTTR?
24. How do queue age and retry volume help?
25. How should sampling affect incident debugging?
26. How should retention reflect operational value?
27. How do you validate recovery using telemetry?
28. How should dashboards support on-call?
29. What observability gaps should become reliability work?
30. What should block production launch?

## Architect

31. What telemetry standards should every service follow?
32. Which context should propagate across services?
33. How should cardinality budgets be governed?
34. Where should sampling occur conceptually?
35. How should retention differ by signal type?
36. How should telemetry privacy/security be governed?
37. What instrumentation overhead is acceptable?
38. How should business signals fit the observability model?
39. What should a default dashboard hierarchy look like?
40. What change markers should be standardized?
41. How should teams connect metrics to traces?
42. How should observability cost be controlled?
43. How should observability maturity be measured?
44. How do you prevent the observability platform from becoming noise at scale?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / operational reasoning
- FD-4: SRE / observability operating-model reasoning
- FD-5: architecture / governance / cost trade-off reasoning

D00-T014 competency target: at least FD-3.
