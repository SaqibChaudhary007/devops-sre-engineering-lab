# D00-T009 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — CI/CD Foundations

1. Why does continuous integration exist?
2. What problem does frequent integration reduce?
3. What does CI mean beyond having a CI server?
4. Why is CI fundamentally a feedback practice?
5. What does continuous delivery mean?
6. What does continuous deployment mean?
7. How are continuous delivery and continuous deployment different?
8. Why is continuous deployment not appropriate for every system?

## Part B — Pipeline Structure

9. What is a pipeline?
10. Why is a pipeline only a mechanism?
11. What is the difference between a pipeline/workflow, job/stage, and step/task?
12. Name common pipeline triggers.
13. Why must a pipeline know the exact source revision?
14. What does a build produce?
15. Why does successful build not prove production safety?
16. Why do different validation layers exist?
17. Why should fast checks usually happen early?
18. What is a quality gate?

## Part C — Artifacts and Promotion

19. What is a release artifact?
20. Give three examples of artifacts.
21. Why should production artifact identity be knowable?
22. What does "build once, promote" mean?
23. Why can rebuilding per environment increase uncertainty?
24. What is artifact immutability?
25. Why is immutable identity useful during incidents?
26. What is an artifact repository?
27. How is artifact promotion different from artifact rebuild?
28. Why can the same artifact still behave differently across environments?
29. What is the difference between an artifact and a cache?
30. Why should a cache not be treated as the canonical release artifact?

## Part D — Deployment and Release

31. What is deployment?
32. What is release?
33. Why are deployment and release not always the same?
34. How can feature flags separate deployment from release?
35. What risks can long-lived feature flags create?
36. What is the purpose of deployment strategy?
37. How can a deployment strategy reduce blast radius?
38. Why should production exposure be controlled independently from build success?

## Part E — Gates, Feedback, Failure Handling

39. What is an approval gate?
40. When is a human approval valuable?
41. When does approval become ritual waiting?
42. What is an automated policy gate?
43. What pipeline feedback should be preserved after failure?
44. Why is blind rerun dangerous?
45. What is a transient failure?
46. What is a deterministic failure?
47. What is a flaky test?
48. Why do flaky tests damage trust in CI?
49. What evidence is needed before deciding to retry?

## Part F — Concurrency, Runners, Caching

50. Why does pipeline concurrency matter?
51. What can happen if two runs deploy to the same environment simultaneously?
52. What can concurrency controls prevent?
53. What can they not guarantee?
54. What is a runner/agent/executor?
55. What is the difference between hosted and self-hosted runners?
56. Why can self-hosted runners increase operational responsibility?
57. Why is runner trust part of pipeline security?
58. What is caching used for?
59. How can stale or poisoned caches create risk?

## Part G — Secrets, Permissions, Environment Protection

60. Why should pipeline credentials be least privilege?
61. Why are broad administrator credentials dangerous in CI/CD?
62. Why should secrets not be hardcoded or printed?
63. What is the advantage of short-lived credentials?
64. What is OIDC/federated identity at a high level?
65. What is environment protection?
66. What controls may protect production environments?
67. Why should branch/tag rules matter for critical delivery paths?

## Part H — Deployment Verification and Observability

68. Why does a successful deploy command not prove service health?
69. What should post-deployment verification include?
70. Why should deployment events appear in production telemetry?
71. What is a change marker?
72. How can change markers help incident diagnosis?
73. Why should CI/CD connect to SLOs?
74. Why does production feedback belong in the delivery loop?

## Part I — Rollback, Roll Forward, Data

75. What is rollback?
76. When is rollback easier?
77. Why can rollback be unsafe?
78. What is roll-forward?
79. When may roll-forward be safer than rollback?
80. Why do database/schema changes complicate recovery?
81. Why should application and data changes be designed together?

## Part J — CI/CD with IaC, GitOps, Supply Chain

82. How can application delivery and IaC delivery interact?
83. What is a push-based CI/CD model?
84. What is a GitOps pull/reconciliation model?
85. Why are CI/CD and GitOps not the same?
86. Why does GitOps not eliminate the need for CI?
87. What is supply-chain provenance at a high level?
88. What can provenance help prove?
89. What can provenance not prove?
90. Why does delivery traceability extend beyond commit SHA?

## Part K — Senior / SRE / Architect Thinking

91. What should a senior engineer inspect when a pipeline is slow?
92. What should an SRE correlate with production deployments?
93. Why is pipeline reliability itself a production concern?
94. How should an architect choose approval and protection boundaries?
95. Why is artifact strategy an architecture decision?
96. Why is CI/CD architecture part of system architecture?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish CI, continuous delivery, and continuous deployment?
- Did I explain build-once/promote clearly?
- Did I distinguish artifacts from caches?
- Did I distinguish deployment from release?
- Did I explain retry/concurrency risk?
- Did I explain why green pipelines are evidence rather than certainty?
- Did I explain rollback limits?
- Did I distinguish CI/CD from GitOps?
