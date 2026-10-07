# D00-T013 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — SRE Foundations

1. What is Site Reliability Engineering?
2. Why does SRE exist?
3. How does SRE differ from purely manual operations?
4. Why is SRE not the same as monitoring?
5. Why is SRE not the same as on-call?
6. Why is SRE not identical to DevOps?
7. What does it mean to apply software engineering to operations?
8. Why is reliability treated as a product feature?

## Part B — Service Boundaries and User Journeys

9. What is a service boundary?
10. Why must the service boundary be explicit?
11. What is a critical user journey?
12. Why should SRE start from user-visible outcomes?
13. Why can infrastructure health be misleading?
14. What makes a good event definition useful?
15. Why should metrics follow user needs rather than metric availability?
16. Why can a dependency outside the team still affect the service SLO?

## Part C — SLI / SLO / SLA

17. What is an SLI?
18. What is an SLO?
19. What is an SLA?
20. Why should SLI, SLO, and SLA not be used interchangeably?
21. Give an availability SLI example.
22. Give a latency SLI example.
23. Give a correctness-oriented SLI example.
24. Give a freshness-oriented SLI example.
25. Why can successful-but-slow requests still violate reliability expectations?
26. Why can a fast response still be unreliable?

## Part D — Error Budgets and Risk

27. What is an error budget?
28. How is it conceptually derived from an SLO?
29. Why does an error budget matter operationally?
30. Why is 100% reliability usually the wrong target?
31. How can error-budget health influence change decisions?
32. Why is one company's freeze policy not a universal SRE standard?
33. What does safe velocity mean?
34. Why is SRE fundamentally a risk-management discipline?

## Part E — Alerting / Paging / Tickets

35. What makes a signal page-worthy?
36. How is a page different from a ticket?
37. What is a dashboard for?
38. Why should not every alert page a human?
39. What is alert fatigue?
40. How can alert fatigue reduce reliability?
41. Why is CPU > 80% often weak paging logic by itself?
42. What is the difference between a symptom and a cause?
43. Why should user-impact symptoms receive high priority?
44. Why should alert actionability matter?

## Part F — On-Call and Operational Load

45. What is on-call?
46. What makes an on-call system sustainable?
47. Why is on-call pain a feedback signal?
48. What recurring problems should become engineering work?
49. How can unclear ownership increase incident duration?
50. Why do access and runbooks matter during on-call response?
51. What happens if page volume grows with service scale?
52. Why is permanent firefighting not a mature SRE model?

## Part G — Toil and Automation

53. What is toil?
54. Why is toil not the same as unpleasant work?
55. Name several characteristics of toil.
56. Why does toil become a scaling problem?
57. Give one example of operational work that is not clearly toil.
58. Why should automation follow understanding?
59. How can automation increase blast radius?
60. What should safe automation include?
61. When should human judgment remain involved?
62. Why is one-time engineering work not automatically toil?

## Part H — Incident Response

63. What is an incident?
64. What is the first goal during a major incident?
65. What is mitigation?
66. What is permanent/root-cause correction?
67. Why can mitigation come before full root-cause understanding?
68. What are useful incident timeline stages?
69. Why should recovery be validated?
70. What should prove that user impact has ended?

## Part I — Postmortems and Learning

71. What is a postmortem?
72. What should a strong postmortem analyze?
73. What does blameless learning mean?
74. Why does blameless not mean accountability-free?
75. Why is "be more careful next time" a weak action item?
76. What makes a good reliability action item?
77. How should repeated incident patterns change engineering priorities?
78. Why are postmortems part of reliability engineering rather than administration?

## Part J — Release Engineering and Safe Change

79. Why does release engineering matter to SRE?
80. What is progressive delivery?
81. What is a canary release at a high level?
82. Why can canarying reduce blast radius?
83. Why does canarying not prove correctness?
84. What signals are needed during progressive rollout?
85. When might rollback be unsafe?
86. Why does roll-forward remain an important recovery option?

## Part K — Capacity and Production Readiness

87. Why is capacity part of reliability?
88. What is capacity headroom?
89. Why can retry traffic consume headroom?
90. What is overload protection?
91. Why can serving fewer requests well be safer than serving all requests badly?
92. What should production readiness include?
93. Why is ownership part of production readiness?
94. Why should dependency reliability be considered end to end?
95. Why should reliability be reviewed continuously?
96. What is the strongest single idea you should retain from D00-T013?

## Self-Check

Before reviewing the rubric, ask:

- Did I define SRE as an engineering operating model?
- Did I anchor SRE to user journeys and service objectives?
- Did I distinguish SLI/SLO/SLA/error budget?
- Did I distinguish page/ticket/dashboard?
- Did I classify toil carefully?
- Did I separate mitigation from permanent correction?
- Did I explain blameless learning correctly?
- Did I explain why canarying reduces risk but does not prove correctness?
