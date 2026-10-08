# D00-T018 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Failure Foundations

1. What is a fault?
2. What is an error or degraded internal state?
3. What is a failure?
4. Why can terminology vary across reliability disciplines?
5. What is a failure mode?
6. Why is "service failed" too vague?
7. What is impact?
8. Why should failure be connected to user or business outcomes?

## Part B — Failure Types

9. What is a transient failure?
10. What is a permanent or non-transient failure?
11. What is an intermittent failure?
12. What is a partial failure?
13. What is a gray or observer-dependent failure?
14. Why can slow behavior be a failure mode?
15. Why can stale data be a failure?
16. Why can incorrect data be worse than an explicit error?

## Part C — Failure Domains and Blast Radius

17. What is a failure domain?
18. What is blast radius?
19. Why is blast radius relative to the failure being considered?
20. Give five possible failure-domain boundaries.
21. Why can replicas share one effective failure domain?
22. What is correlated failure?
23. What is common-mode failure?
24. What is a hidden shared dependency?

## Part D — Dependencies and Propagation

25. How can a healthy service fail because of a dependency?
26. Why should dependencies be classified as critical, degradable, optional, or asynchronous?
27. What is failure propagation?
28. Give four propagation paths.
29. What is cascading failure?
30. What is failure amplification?
31. Why can fan-out increase blast radius?
32. Why can shared resource pools spread failure?

## Part E — Overload and Resource Exhaustion

33. What is overload?
34. What is saturation?
35. Give six resources that can be exhausted.
36. Why is human attention also a resource?
37. Why can overload create a reinforcing loop?
38. Why can accepting all work make recovery slower?
39. What is load shedding?
40. Why can rejecting some work improve reliability?

## Part F — Timeout, Retry, Backoff

41. What is a timeout boundary?
42. Why can long waits spread saturation?
43. What is fail-fast behavior?
44. When can fail-fast protect the system?
45. Why can retries recover transient faults?
46. Why can retries amplify failure?
47. Why should retries be bounded?
48. Why do backoff and jitter matter?

## Part G — Backpressure and Graceful Degradation

49. What is backpressure?
50. Why must backpressure propagate upstream?
51. What is graceful degradation?
52. Why must optional functionality be identified before an incident?
53. What is an isolation/bulkhead concept?
54. What problem can isolation reduce?
55. What is a circuit breaker?
56. Why is a circuit breaker not a universal fix?

## Part H — Redundancy, Failover, Failback

57. What is redundancy?
58. Why is redundancy not the same as independence?
59. What is failover?
60. What assumptions must hold for failover to succeed?
61. Why can failover itself fail?
62. What is failback?
63. Why can failback reintroduce instability?
64. What is the foundation-level difference between active/active and active/passive?

## Part I — Data Recovery and DR

65. Why is data failure different from process failure?
66. Why does backup existence not prove recoverability?
67. What must be validated after a restore?
68. What is RTO?
69. What is RPO?
70. Why are RTO and RPO different?
71. Why should recovery objectives be business-driven?
72. Why should recovery procedures be tested?

## Part J — Partitions, State Uncertainty, Duplicates

73. What is a network partition?
74. Why is exact partition behavior protocol-specific?
75. What is split-brain at a foundation level?
76. What is quorum at a foundation level?
77. What is state uncertainty?
78. Why can a timeout leave outcome unknown?
79. How do idempotency and operation identity help?
80. Why can retries create duplicate processing?

## Part K — Change, Humans, Observability

81. Why are changes a common source of failure?
82. How can configuration fail independently of code?
83. How can security controls affect reliability?
84. Why is "human error" an incomplete explanation?
85. How can observability itself fail?
86. How can alerting fail?
87. How can a runbook fail?
88. Why does control-plane vs data-plane distinction matter?

## Part L — Containment, Recovery, Testing

89. What is containment?
90. Why can containment precede perfect explanation?
91. What is recovery validation?
92. Why is one green metric not enough?
93. What is a pre-mortem?
94. What is a game day?
95. What makes failure testing safe and useful?
96. Why is chaos engineering not random destruction?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish fault, error/degradation, failure, and impact?
- Did I identify more than up/down failure modes?
- Did I reason about failure domains and blast radius?
- Did I understand retry amplification?
- Did I understand overload protection?
- Did I distinguish redundancy from independence?
- Did I distinguish backup from recovery?
- Did I understand RTO vs RPO?
- Did I keep partition/quorum reasoning protocol-specific?
- Did I define recovery validation and safe failure-testing boundaries?
