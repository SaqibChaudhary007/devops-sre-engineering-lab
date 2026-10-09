# D00-T018 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Failure Foundations

1. What is a fault?
2. What is an error or degraded internal state?
3. What is a failure?
4. Why can fault/error/failure terminology vary by discipline?
5. What is a failure mode?
6. Why is "service failed" too vague?
7. What is impact?
8. Why should failure always be connected to observable impact?

## Part B — Failure Types

9. What is a transient failure?
10. What is a permanent or non-transient failure?
11. What is an intermittent failure?
12. What is a partial failure?
13. What is an observer-dependent or gray failure?
14. Why can slow behavior be a failure mode?
15. Why can stale data be a failure?
16. Why can incorrect data be worse than an explicit error?

## Part C — Failure Domains and Blast Radius

17. What is a failure domain?
18. What is blast radius?
19. Why are failure domains relative to the failure being considered?
20. Give five possible failure domains.
21. What is correlated failure?
22. What is common-mode failure?
23. Why can redundancy fail to provide independence?
24. What is a hidden shared dependency?

## Part D — Dependency and Overload Failure

25. How can a dependency fail without being fully down?
26. Why does end-to-end reliability belong to the user journey?
27. What is overload failure?
28. What is resource exhaustion?
29. Give six examples of resources that can be exhausted.
30. What is cascading failure?
31. What is failure propagation?
32. What is failure amplification?

## Part E — Timeouts, Retries, and Pressure Control

33. Why are timeout boundaries important?
34. What does fail-fast mean?
35. When can fail-fast behavior improve reliability?
36. Why can retries amplify failure?
37. Why can multiple retry layers multiply work?
38. Why should retries be bounded?
39. What is the role of backoff?
40. What is the role of jitter?

## Part F — Load Shedding, Backpressure, Degradation

41. What is load shedding?
42. Why can rejecting some work improve overall availability?
43. What is backpressure?
44. Why must backpressure propagate upstream?
45. What is graceful degradation?
46. Why does graceful degradation require business/product understanding?
47. What is a critical dependency?
48. What is a degradable or optional dependency?

## Part G — Isolation, Circuit Breakers, Redundancy

49. What is isolation or a bulkhead conceptually?
50. How can isolation reduce blast radius?
51. What is a circuit breaker?
52. Why is a circuit breaker not a universal fix?
53. What is redundancy?
54. Why is redundancy not the same as independence?
55. What is failover?
56. Why can failover itself fail?

## Part H — Recovery and Data Resilience

57. What is failback?
58. Why can failback be risky?
59. What is data failure?
60. Why is service restart different from data recovery?
61. Why does a backup not prove recovery?
62. What must be validated after restore?
63. What is RTO?
64. What is RPO?

## Part I — Distributed State and Uncertainty

65. What is a network partition?
66. Why can partition behavior differ by protocol?
67. What is split-brain at a conceptual level?
68. What is quorum at a conceptual level?
69. Why should etcd-style majority behavior not be generalized to all systems?
70. What is state uncertainty?
71. Why is unknown outcome dangerous for side-effecting operations?
72. How do operation identity and idempotency help?

## Part J — Change, Human, and Operational Failure

73. Why are changes a major failure source?
74. Give four examples of configuration failure.
75. How can security controls create reliability failures?
76. Why should incidents not be reduced to "human error"?
77. What is observability failure?
78. What is alerting failure?
79. What is runbook failure?
80. Why does control-plane vs data-plane distinction matter?

## Part K — Detection, Containment, Recovery, Learning

81. What should failure detection answer?
82. What is containment?
83. Why can containment be more urgent than perfect explanation?
84. What is recovery?
85. Why is one green metric insufficient to declare recovery?
86. What should recovery validation include?
87. What is a pre-mortem?
88. Why is learning part of failure handling?

## Part L — Failure Testing and Resilience

89. What is failure testing?
90. What is fault injection at a foundation level?
91. What is chaos engineering?
92. Why is chaos engineering not random destruction?
93. What is a game day?
94. Why are stop conditions important in failure experiments?
95. Why must failure testing be authorized and bounded?
96. What is the strongest idea you should retain from D00-T018?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish failure types rather than use only up/down thinking?
- Did I identify failure domains and blast radius?
- Did I treat retries as part of failure propagation?
- Did I distinguish redundancy from independence?
- Did I distinguish backup from proven recovery?
- Did I keep partition/quorum behavior protocol-specific?
- Did I require end-to-end recovery validation?
- Did I preserve safe, bounded, hypothesis-driven failure-testing principles?
