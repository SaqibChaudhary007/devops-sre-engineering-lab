# D00-T015 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Security and Risk

1. What is security engineering?
2. Why is security fundamentally a risk-management discipline?
3. What does confidentiality mean?
4. What does integrity mean?
5. What does availability mean?
6. Why is the CIA triad useful but incomplete?
7. What is an asset?
8. Why should assets be identified before choosing controls?

## Part B — Threats, Vulnerabilities, Risk, Attack Surface

9. What is a threat?
10. What is a vulnerability?
11. How are threat and vulnerability different?
12. What is a threat actor?
13. Why must accidental causes be included in security thinking?
14. What is attack surface?
15. Why does unnecessary exposure increase security responsibility?
16. Why is risk ≈ likelihood × impact only a beginner model?

## Part C — Trust Boundaries and Identity

17. What is a trust boundary?
18. Why should crossing a trust boundary trigger explicit security decisions?
19. What is identity?
20. What is human identity?
21. What is workload/service identity?
22. Why should humans and workloads generally not share identity?
23. Why is network location alone not a sufficient trust signal?
24. What does Zero Trust mean at a foundation level?

## Part D — Authentication, Authorization, Least Privilege

25. What is authentication?
26. What is authorization?
27. Why are authentication and authorization different?
28. Why can a strongly authenticated identity still be dangerous?
29. What is least privilege?
30. How do scope and duration strengthen least privilege?
31. What is separation of duties?
32. What is deny-by-default?
33. Why is time-bounded access useful?
34. How does least privilege reduce blast radius?

## Part E — Credentials and Secrets

35. What is a credential?
36. What is a secret?
37. Why should secrets not be treated as ordinary configuration?
38. What are the major stages of a secret lifecycle?
39. Why are hard-coded secrets dangerous?
40. Why can repository history make secret exposure long-lived?
41. Why are short-lived credentials useful?
42. Why are short-lived credentials not automatically safe?
43. Why should workload credentials be scoped?
44. Why should secret access be audited?

## Part F — Encryption, Hashing, Certificates, Data

45. What does encryption in transit protect?
46. What does encryption at rest protect?
47. Why does encryption not replace authorization?
48. What is hashing at a high level?
49. Why is hashing different from reversible encryption?
50. Why should plain SHA-256 not be taught as sufficient password storage?
51. What is a certificate at a foundation level?
52. What is data classification?
53. How can data classification affect access and retention?
54. What is data minimization?

## Part G — Audit, Detection, Defense in Depth, Defaults

55. What should a useful audit trail answer?
56. Why is security monitoring necessary even with preventive controls?
57. What does prevent → detect → contain → recover → learn represent?
58. What is defense in depth?
59. Why does defense in depth not mean adding random controls?
60. What are secure defaults?
61. What are fail-safe defaults?
62. Why can insecure configuration be as dangerous as software defects?

## Part H — Hardening, Patching, Vulnerability Management

63. What is hardening?
64. Why should hardening follow system purpose?
65. Why is patching a security and operational activity?
66. Why should urgent patches still be deployed safely?
67. What is vulnerability management?
68. Why should vulnerability priority not depend on severity score alone?
69. How do asset value and exposure affect vulnerability priority?
70. What is the role of exceptions in vulnerability management?

## Part I — Dependencies, Supply Chain, CI/CD, IaC

71. Why does every dependency extend the trust chain?
72. What is third-party risk?
73. What is the software-supply-chain path at a high level?
74. What is artifact integrity?
75. What is provenance?
76. Why is provenance not automatic trust?
77. Why is CI/CD a security-sensitive trust boundary?
78. How can overly broad pipeline permissions increase blast radius?
79. How can IaC improve security?
80. How can IaC spread insecure configuration quickly?

## Part J — Cloud, Segmentation, Recovery

81. What does cloud shared responsibility mean?
82. Why does shared responsibility vary by service model?
83. What customer responsibilities commonly remain even with managed services?
84. What is network segmentation at a high level?
85. How does segmentation reduce lateral blast radius?
86. Why are backups a security asset?
87. Why should backup deletion/restore permissions be tightly controlled?
88. Why should recovery credentials be reviewed separately from production access?

## Part K — Operations, Reliability, Production Readiness

89. How do security and observability reinforce each other?
90. How can security controls conflict with reliability?
91. Why can poor emergency-access design slow recovery?
92. Why can excessive privilege turn a reliability incident into a security incident?
93. Why should the secure path be the easy path?
94. Why must security ownership be explicit?
95. Why is security a production-readiness gate?
96. What is the strongest single idea you should retain from D00-T015?

## Self-Check

Before reviewing the rubric, ask:

- Did I start from assets and meaningful risk?
- Did I distinguish authentication from authorization?
- Did I apply least privilege to scope and duration?
- Did I treat secrets as lifecycle assets?
- Did I avoid treating encryption as a universal solution?
- Did I explain Zero Trust without "trust nobody"?
- Did I treat CI/CD and supply chain as trust boundaries?
- Did I explain provenance as evidence rather than automatic trust?
- Did I include detection, response, and recovery?
- Did I balance security with reliability?
