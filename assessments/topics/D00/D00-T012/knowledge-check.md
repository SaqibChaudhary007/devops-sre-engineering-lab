# D00-T012 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Reliability Foundations

1. What is reliability?
2. Why is reliability broader than uptime?
3. What is availability?
4. What is durability?
5. What is resilience?
6. What is fault tolerance?
7. What is recoverability?
8. Why should reliability be user-centered?

## Part B — User Journeys and Failure Models

9. What is a critical user journey?
10. Why can component health be misleading?
11. What is a failure model?
12. Why must reliability claims name the failures they tolerate?
13. What is a failure domain?
14. What is blast radius?
15. Why can one failure affect multiple components at once?
16. Why should blast radius be limited?

## Part C — Redundancy and Degradation

17. What is redundancy?
18. Why is redundancy not sufficient by itself?
19. Why does independence matter?
20. Why can two replicas on one host still be one failure domain?
21. What is graceful degradation?
22. When is graceful degradation appropriate?
23. When would graceful degradation violate correctness?
24. What is failover?

## Part D — Detection and Recovery

25. What is detection time?
26. What is response time?
27. What is recovery time?
28. Why can slow detection dominate incident duration?
29. What is MTTR at a high level?
30. Why must MTTR be defined explicitly?
31. Why can averages hide severe incidents?
32. Why should recovery be designed rather than improvised?

## Part E — SLI, SLO, SLA, Error Budget

33. What is an SLI?
34. What is an SLO?
35. What is an SLA?
36. Why should SLI/SLO/SLA not be used interchangeably?
37. What is an error budget?
38. How is an error budget conceptually related to an SLO?
39. Why should an error budget influence engineering decisions?
40. Why is 100% reliability usually the wrong default target?

## Part F — Reliability Targets and Cost

41. Why do different services need different reliability targets?
42. What business factors influence a reliability target?
43. Why can higher reliability cost disproportionately more?
44. Why is reliability an engineering and business trade-off?
45. Why can one external dependency dominate end-to-end reliability?
46. What does end-to-end reliability mean?

## Part G — Health, Observability, and Alerts

47. Why is process liveness not enough to prove service health?
48. What signals can represent service health?
49. Why is observability important for reliability?
50. Why is observability not the same as reliability?
51. What makes an alert actionable?
52. Why can a CPU-only alert be weak?
53. What is the difference between symptom and cause?
54. Why should user-impact symptoms be prioritized?

## Part H — Change and Deployment Risk

55. Why is change a reliability risk?
56. Give four kinds of change that can cause incidents.
57. Why can smaller changes reduce risk?
58. What is rollback?
59. What is roll-forward?
60. When can rollback be unsafe?
61. Why do schema/data compatibility matter during recovery?
62. Why should recovery strategy be considered before deployment?

## Part I — Capacity and Overload

63. What is capacity headroom?
64. Why does failover require spare capacity?
65. What is saturation?
66. How can saturation create cascading failure?
67. What is load shedding?
68. Why can rejecting some work preserve reliability?
69. What is backpressure?
70. Why do queues not create infinite capacity?

## Part J — Backup, RTO, RPO, DR

71. Why is backup not the same as recovery?
72. What is a restore test proving?
73. What is RTO?
74. What is RPO?
75. Why are RTO and RPO different?
76. Why does a backup every 15 minutes not automatically prove an RPO of 15 minutes?
77. What is disaster recovery at a high level?
78. Why should DR be tested rather than documented only?

## Part K — Incident Readiness and Human Factors

79. What is a runbook?
80. What should a good runbook contain?
81. Why does ownership matter during incidents?
82. Why do permissions and access affect recovery time?
83. What is toil at a high level?
84. Why can excessive toil reduce reliability?
85. Why should automation itself be reliable?
86. What is production readiness?

## Part L — Senior / SRE / Architect Reasoning

87. Why should reliability start with the user journey?
88. Why should replicas be evaluated against failure domains?
89. Why can graceful degradation improve SLO performance?
90. Why can alert quality affect MTTR?
91. Why does capacity headroom matter during node loss?
92. Why is tested recovery stronger evidence than backup success?
93. Why should reliability targets reflect business value?
94. Why should failover success be validated?
95. Why is reliability continuous rather than a one-time project?
96. What does a strong reliability engineer optimize beyond failure prevention?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish reliability, availability, durability, resilience, and recoverability?
- Did I anchor reliability to a critical user journey?
- Did I explain failure domains and correlated redundancy?
- Did I distinguish SLI, SLO, SLA, and error budget?
- Did I distinguish backup from proven recovery?
- Did I explain RTO and RPO separately?
- Did I connect capacity headroom to failover?
- Did I explain detection, response, and recovery as different intervals?
