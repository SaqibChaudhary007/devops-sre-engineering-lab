# D00-T006 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What changes when infrastructure becomes API-driven?
2. How would you explain control plane vs data plane during an incident?
3. How would you prove whether a failure is management-path or workload-path?
4. What is the difference between scalability and elasticity?
5. Why can autoscaling increase pressure on a failing dependency?
6. How do quotas create hidden scaling ceilings?
7. Why can a managed service still require customer observability?
8. How do you determine what is ephemeral and what must persist?
9. Why can local application state break horizontal scaling?
10. What evidence do you need before calling a workload multi-zone?
11. Why is multi-zone not the same thing as DR?
12. What makes a public-cloud workload private even though it runs in public cloud?
13. What responsibility remains with the customer in SaaS?
14. Why can cloud cost anomalies be symptoms of architecture problems?

## SRE

15. Which SLIs matter more: portal availability or user-path availability?
16. What autoscaling signals are risky if used alone?
17. How would you monitor quota consumption?
18. How do you detect failed or stuck scaling activity?
19. How does zone placement influence SLO risk?
20. How would you test failover without assuming capacity exists?
21. What does dependency saturation look like when app CPU is normal?
22. How should control-plane change events be used during incident investigation?
23. Why is cloud cost useful as an operational signal?
24. What is a meaningful blast-radius taxonomy for cloud incidents?
25. How can provider limits affect recovery?
26. What evidence is required before claiming resilience?

## Architect

27. When would IaaS be preferable to a higher-level managed service?
28. When would PaaS be the better trade-off?
29. When would serverless be a poor fit?
30. How do availability and recovery requirements influence region/zone strategy?
31. What does shared responsibility change in security architecture?
32. How do you decide whether state should be externalized?
33. How do you design autoscaling around downstream capacity?
34. When is multi-region justified?
35. When is multi-cloud justified?
36. How do you avoid creating portability complexity with no business value?
37. How do quotas influence architecture planning?
38. How do governance and self-service coexist?
39. How should cloud identity be designed for automation?
40. Why is cloud-native an operating model rather than a Kubernetes synonym?
41. How should cost influence resilience design?
42. What trade-offs exist between provider-native managed services and portability?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting/failure reasoning
- FD-4: reliability/operations
- FD-5: architecture/trade-offs

D00-T006 competency target: at least FD-3.
