# D00-T009 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Why does CI exist?
2. Why does frequent integration reduce risk?
3. How do continuous delivery and continuous deployment differ?
4. Why is a pipeline tool not equivalent to delivery maturity?
5. What is the difference between a stage, job, and step?
6. Why does exact source revision matter?
7. Why does successful build not prove production safety?
8. Why do fast checks belong early?
9. What makes a quality gate meaningful?
10. Why is build-once/promote useful?
11. Why can the same artifact behave differently across environments?
12. Artifact vs cache: what is the operational difference?
13. Why should artifact identity be immutable?
14. Why are deployment and release separate concepts?
15. When are feature flags useful?
16. When do feature flags create risk?
17. Why is blind retry unsafe?
18. How do you diagnose a flaky test?

## SRE

19. Why should deployments appear in telemetry?
20. How do change markers improve incident response?
21. What does a failed deployment recovery metric tell you?
22. Why can pipeline reliability affect service reliability?
23. How can concurrency create a production incident?
24. What post-deployment signals matter most?
25. When should automation stop rather than retry?
26. When is rollback unsafe?
27. When is roll-forward safer?
28. How do database changes affect recovery?
29. What delivery toil would you eliminate first?
30. How can SLOs influence deployment decisions?

## Architect

31. How should you choose environment boundaries?
32. Where should approvals exist?
33. Which gates should be automated?
34. Which decisions still require human judgment?
35. How do you design artifact retention and trust?
36. How should runner trust boundaries be designed?
37. What credentials should production deployment use?
38. How do you limit deployment blast radius?
39. How should application and IaC pipelines coordinate?
40. Where does GitOps fit into the delivery architecture?
41. How do you design concurrency for shared targets?
42. How should deployment and release be decoupled?
43. What evidence should be retained for audit/recovery?
44. How does software supply-chain provenance change your design?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / delivery reasoning
- FD-4: reliability / operational reasoning
- FD-5: architecture / organizational trade-offs

D00-T009 competency target: at least FD-3.
