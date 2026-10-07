# D00-T007 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer short explanations over one-word answers.

## Part A — Why DevOps Exists

1. Why did DevOps emerge?
2. What problems can development/operations silos create?
3. Why is DevOps not a job title by definition?
4. Why can a team called "DevOps" still preserve old silos?
5. What does it mean to optimize the whole delivery system?
6. Why can local team optimization hurt end-to-end delivery?
7. What are shared outcomes in a DevOps-oriented model?
8. Why should customer value and reliability be considered together?

## Part B — Flow

9. What is flow?
10. Write the basic idea-to-production flow.
11. What is lead time?
12. What is batch size?
13. Why can smaller batches improve diagnosability?
14. What is work in progress?
15. Why can excessive WIP reduce throughput?
16. What is a queue?
17. Give four delivery-system queue examples.
18. What is a handoff?
19. Why can handoffs introduce delay or context loss?
20. What is a bottleneck?
21. Why does making a non-bottleneck stage faster often fail to improve system throughput?

## Part C — Feedback

22. What is a feedback loop?
23. Why does fast feedback matter?
24. What kinds of feedback come from CI?
25. What kinds of feedback come from production?
26. Why can lower environments never perfectly reproduce production?
27. Why does production feedback not mean uncontrolled testing in production?
28. What is the difference between detection and learning?

## Part D — Automation, Standardization, Reproducibility

29. What does automation improve?
30. Why can automation amplify a bad decision?
31. What is standardization?
32. How can too much standardization become harmful?
33. What is reproducibility?
34. Why does reproducibility reduce "works on my machine" problems?
35. Why is IaC a DevOps enabler but not DevOps itself?
36. Why should infrastructure changes be reviewable and observable?

## Part E — CI/CD

37. What is continuous integration?
38. Why is CI more than owning a CI tool?
39. What is continuous delivery?
40. What is continuous deployment?
41. What is the main difference between continuous delivery and continuous deployment?
42. Why is a pipeline not the goal?
43. Which outcomes should a delivery pipeline support?
44. Why can a very complex pipeline reduce delivery performance?
45. Why should deployment strategy depend on risk and context?

## Part F — Current DORA Metrics

46. Name the current five DORA software-delivery performance metrics.
47. Which three are grouped under throughput?
48. Which two are grouped under instability?
49. What is deployment frequency?
50. What is change lead time?
51. What is change fail rate?
52. What is failed deployment recovery time?
53. What is deployment rework rate?
54. Why is failed deployment recovery time more precise than the older broad MTTR framing?
55. Why should DORA metrics not be treated as universal targets to game?
56. Why does deployment frequency alone not prove maturity?
57. How can high deployment frequency coexist with poor engineering outcomes?

## Part G — Ownership and Toil

58. What does production ownership mean?
59. What is the nuance behind "you build it, you run it"?
60. What is toil?
61. Name at least four characteristics of toil.
62. Why is not every manual task toil?
63. Why should toil be reduced through engineering?
64. What kinds of work still need human judgment?
65. Why does ownership not mean one person must do everything?

## Part H — Observability, Security, and Change

66. Why is observability part of the DevOps feedback loop?
67. What is shift left?
68. What is shift right?
69. Why are shift left and shift right complementary?
70. Why does environment drift create risk?
71. Why can configuration changes cause incidents without code changes?
72. What should good change management ask before production change?
73. Why does DevOps not mean removing all change controls?
74. What is rollback?
75. What is roll forward?
76. Why should recovery be designed before an incident?

## Part I — Learning Culture

77. What does blameless learning mean?
78. Why does blameless not mean no accountability?
79. What questions should a strong post-incident review ask?
80. Why are durable action items important?
81. What happens when incidents produce no system improvement?

## Part J — DevOps, SRE, Platform Engineering

82. How is DevOps different from SRE?
83. How can SRE implement DevOps principles?
84. Why are DevOps and SRE not identical?
85. What is platform engineering?
86. How can platform engineering scale DevOps practices?
87. Why does platform engineering not replace ownership and feedback?
88. Why does owning Kubernetes/Terraform/CI tools not prove DevOps maturity?

## Part K — Senior / SRE / Architect Thinking

89. What should a senior engineer inspect first when delivery is slow?
90. Why should an SRE correlate deployments with SLO impact?
91. Why should an architect include the path to production in system design?
92. Why can organizational boundaries become architecture constraints?
93. When can standardization improve delivery?
94. When can standardization become too rigid?
95. Why can smaller changes improve both speed and safety?
96. Why should a delivery system optimize recovery as well as prevention?

## Self-Check

Before reviewing the rubric, ask:

- Did I explain DevOps without naming tools?
- Did I reason about queues, WIP, handoffs, and bottlenecks?
- Did I distinguish CI, continuous delivery, and continuous deployment?
- Did I use the current five DORA metrics correctly?
- Did I explain toil precisely?
- Did I explain blameless learning without removing accountability?
- Did I distinguish DevOps, SRE, and platform engineering?
