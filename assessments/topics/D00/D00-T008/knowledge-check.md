# D00-T008 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Why IaC Exists

1. Why does Infrastructure as Code exist?
2. What problems arise from one-off manual infrastructure changes?
3. Why is IaC more than "automation"?
4. Why is IaC not equivalent to Terraform?
5. What does it mean to make infrastructure changes reviewable?
6. Why does traceability matter for infrastructure?
7. Why does repeatability matter?
8. Why can automation increase both speed and risk?

## Part B — Desired vs Actual State

9. What is desired state?
10. What is actual state?
11. Why can desired state and actual state differ?
12. What is reconciliation?
13. Why does not every IaC tool continuously reconcile?
14. What is configuration drift?
15. Give three causes of drift.
16. Why is drift a security risk?
17. Why is drift a troubleshooting risk?
18. Why is the repository not the same as runtime truth?

## Part C — Declarative, Imperative, Idempotence

19. What is a declarative approach?
20. What is an imperative approach?
21. Why is declarative not automatically better?
22. What is idempotence?
23. Why is idempotence desirable for infrastructure automation?
24. Why must idempotence be qualified by tool/module implementation?
25. How can an imperative workflow still be reliable?
26. Can declarative infrastructure express unsafe intent? Explain.

## Part D — Version Control, Diff, Plan, Apply

27. Why put infrastructure definitions in version control?
28. What does a code diff show?
29. Why can a code diff fail to show full runtime impact?
30. What is a plan/preview/change set?
31. Name common actions a plan may show.
32. Why does a plan reduce uncertainty?
33. Why does a plan not guarantee execution success?
34. What does apply do?
35. Why is apply the point where blast radius becomes real?
36. Why should production apply controls differ from development?

## Part E — Resource Lifecycle and Replacement

37. Name common infrastructure lifecycle actions.
38. What is the difference between update and replacement?
39. Why can replacement be dangerous?
40. What questions should be asked before replacing a stateful resource?
41. Why can an apparently small property change trigger replacement?
42. Why can resource identity changes matter?
43. Why can delete be more dangerous than update?
44. Why should deletion of stateful resources require stronger evidence?

## Part F — Dependencies

45. What is a dependency graph?
46. Why does dependency order matter?
47. What is an implicit dependency?
48. What is an explicit dependency?
49. Why can overusing explicit dependencies be harmful?
50. What can happen if dependency ordering is wrong?

## Part G — State

51. What problem does Terraform state solve?
52. Why is explicit state not universal across IaC systems?
53. Which mental concept is more universal than "state file"?
54. Why can stale or incorrect state be dangerous?
55. What is remote state?
56. Why might teams use remote state?
57. Why is remote state not automatically equivalent to safe locking?
58. What does state locking protect against?
59. What does locking not solve?
60. Why can state be security-sensitive?

## Part H — Variables, Outputs, Modules, Environments

61. What is a variable?
62. What is an output?
63. Why can outputs expose sensitive information?
64. What is a reusable IaC module/component?
65. What are benefits of modules?
66. What are risks of over-generalized modules?
67. Why does module versioning matter?
68. Why should environments not necessarily be identical?
69. What is the risk of too much duplication?
70. What is the risk of too much parameterization?

## Part I — Ownership, Blast Radius, Policy, Secrets

71. Why do state/package ownership boundaries matter?
72. Why can one global state create large blast radius?
73. Name reasonable boundaries for splitting IaC ownership.
74. What should an infrastructure code review ask?
75. What is policy as code?
76. Name three policy-as-code examples.
77. Why should plaintext secrets not be embedded casually in IaC?
78. Why do apply/destroy permissions need strong access control?

## Part J — Provider, API, Import, Destroy

79. What is the provider/plugin mental model?
80. Why can a correct definition still fail to apply?
81. What is import/adoption?
82. Why does import not reconstruct original design intent?
83. Why must imported resources be reviewed with a plan?
84. What is destroy?
85. Why do destructive operations need safeguards?

## Part K — Rollback, GitOps, Senior/SRE/Architect Thinking

86. Why does reverting Git not guarantee infrastructure rollback?
87. What is roll-forward?
88. How is GitOps more specific than IaC?
89. What should a senior engineer verify before apply?
90. What should an SRE correlate with infrastructure changes?
91. Why is IaC architecture partly organizational architecture?
92. How can state boundaries affect incident blast radius?
93. Why should emergency manual changes be reconciled back into code?
94. Why can cost be an IaC architecture concern?
95. Why can a valid plan still be financially unsafe?
96. Why should infrastructure changes be observable?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish desired state from actual state?
- Did I explain drift precisely?
- Did I distinguish declarative from continuous reconciliation?
- Did I explain why state files are tool-specific?
- Did I explain locking as backend/tool-dependent?
- Did I distinguish preview from guaranteed execution?
- Did I explain replacement, deletion, and rollback risk?
- Did I distinguish IaC from GitOps?
