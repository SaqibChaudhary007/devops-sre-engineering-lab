# D00-T016 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Automation Foundations

1. What is automation?
2. Why does automation exist?
3. Why is automation more than scripting?
4. What kinds of work are strong automation candidates?
5. When may manual execution still be appropriate?
6. Why can poor automation increase blast radius?
7. What does it mean to say automation is a force multiplier?
8. Why should task understanding come before automation?

## Part B — Intent, Trigger, and State

9. What is automation intent?
10. What is a trigger?
11. Name four common trigger types.
12. Why does a trigger not prove an action is safe?
13. What is current state?
14. What is desired state?
15. Why must automation reason about state?
16. What problems can stale state create?

## Part C — Reconciliation and Control Loops

17. What is reconciliation?
18. What is a control loop?
19. What are the core steps in a control loop?
20. Why is reconciliation iterative?
21. Why can observed state lag real state?
22. What is drift?
23. How can automation respond to drift?
24. Why is reconciliation not only a Kubernetes concept?

## Part D — Imperative vs Declarative

25. What is imperative automation?
26. What is declarative automation?
27. When is imperative automation useful?
28. When is declarative automation useful?
29. Why is neither universally better?
30. What does convergence mean at a high level?
31. What is push automation?
32. What is pull automation?

## Part E — Preconditions, Postconditions, Validation

33. What is a precondition?
34. Give four examples of preconditions.
35. What is a postcondition?
36. Why are postconditions important?
37. Why is exit code 0 not enough?
38. What is outcome validation?
39. What kinds of evidence can validate outcome?
40. Why should validation match the original intent?

## Part F — Repeatability and Idempotency

41. What is repeatability?
42. What is idempotency?
43. Why are repeatability and idempotency different?
44. Why is idempotency valuable for retries?
45. Why does idempotency not guarantee success?
46. Give an example of an idempotent operation.
47. Give an example of a side-effect-sensitive operation.
48. Why should duplicate execution be expected?

## Part G — Retries, Backoff, Jitter, Timeouts

49. What is a retry?
50. When can retries improve reliability?
51. When can retries make an incident worse?
52. Why should retry be a policy rather than an instinct?
53. What is backoff?
54. Why is backoff useful?
55. What is jitter?
56. Why does jitter reduce synchronized retry storms?
57. What is a timeout?
58. Why should timeout be designed with an overall operation budget?
59. Why can infinite retry hide persistent failure?
60. What should cause retry to stop?

## Part H — Partial Failure and Recovery

61. What is partial failure?
62. Why must workflows assume partial completion?
63. What is rollback?
64. Why is rollback not always safe?
65. What is roll-forward?
66. What is a compensating action?
67. How is compensation different from true rollback?
68. What should happen when outcome is unknown after timeout?

## Part I — Workflows, Queues, Concurrency

69. What is a workflow?
70. What is orchestration?
71. Why does orchestration create coordination state?
72. What benefit do queues provide?
73. What new problems do queues introduce?
74. What is a dead-letter path?
75. What is concurrency?
76. What is a race condition?
77. Why can multiple workers cause conflicting updates?
78. What is locking at a conceptual level?
79. Why can locking itself create failure modes?
80. Why are rate limits useful?

## Part J — Guardrails, Identity, Observability

81. What is automation blast radius?
82. Name five blast-radius guardrails.
83. What is a human approval boundary?
84. Why is human-in-the-loop not anti-automation?
85. Why does automation need its own identity?
86. Why should automation use least privilege?
87. Why are shared human credentials weak automation design?
88. What should automation audit evidence answer?

## Part K — Self-Healing, Readiness, Economics, AI

89. What is self-healing at a foundation level?
90. Why must self-healing be bounded?
91. What makes a good auto-remediation candidate?
92. Why should unknown incidents often escalate to a human?
93. What is the maturity path from runbook to automation?
94. Why does automation have engineering and maintenance cost?
95. How should AI-assisted automation change as impact and uncertainty rise?
96. What is the strongest single idea you should retain from D00-T016?

## Self-Check

Before reviewing the rubric, ask:

- Did I reason about state before action?
- Did I distinguish repeatability from idempotency?
- Did I treat retries as bounded policy?
- Did I account for partial failure and duplicate execution?
- Did I define validation after action?
- Did I include guardrails and human approval?
- Did I give automation explicit identity and least privilege?
- Did I keep self-healing bounded and observable?
