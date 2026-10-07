# D00-T011 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Distributed-System Foundations

1. What makes a system distributed?
2. Why do systems become distributed?
3. What new uncertainty appears when a local call becomes a network call?
4. What is partial failure?
5. Why is partial failure harder than a whole-process failure?
6. Why does distribution not automatically mean scalability?
7. Why can distribution increase operational complexity?
8. What does independent failure mean?

## Part B — Latency, Timeouts, Ambiguity

9. What contributes to remote-call latency?
10. What is tail latency?
11. Why can p95/p99 matter more than average latency?
12. What is a timeout?
13. Why is a timeout not proof that the remote operation failed?
14. What are three possible realities behind one timeout?
15. What happens if timeout values are too short?
16. What happens if timeout values are too long?

## Part C — Retries, Idempotency, Duplicates

17. Why do systems retry?
18. When can retries help?
19. When can retries make an outage worse?
20. What is retry amplification?
21. Why can retries at multiple layers multiply traffic?
22. What is idempotency?
23. Why is request identity important?
24. Why is charging a card harder to retry safely than reading a product?
25. How can duplicate work occur after response loss?
26. What is an idempotency key trying to achieve?
27. Why should retry ownership be explicit?
28. What is a retry budget?

## Part D — Backoff, Jitter, Circuit Breaker, Bulkhead

29. What is exponential backoff?
30. Why can backoff reduce overload?
31. What is jitter?
32. Why can backoff without jitter still synchronize clients?
33. What does a circuit breaker do?
34. What does a circuit breaker not do?
35. How is circuit breaker behavior different from retry?
36. What is a bulkhead?
37. How can bulkheads limit blast radius?
38. What is load shedding?

## Part E — Delivery Semantics and Ordering

39. What does at-most-once mean at a high level?
40. What does at-least-once mean at a high level?
41. Why can at-least-once delivery create duplicates?
42. What does exactly-once delivery mean only within a defined system scope?
43. Why is exactly-once business effect still an end-to-end concern?
44. Why are ordering guarantees scoped?
45. Give one example of an ordering scope.
46. Why is wall-clock time not a perfect global ordering mechanism?

## Part F — Replication and Consistency

47. What is replication?
48. What benefits can replication provide?
49. What new problems can replication create?
50. What is replication lag?
51. What is a stale read?
52. What is eventual consistency?
53. Why is eventual consistency not the same as incorrect data?
54. Why are consistency requirements business requirements?
55. Why might stale recommendations be acceptable?
56. Why might stale payment balances be unacceptable?

## Part G — Partitions, CAP, Failure Detection

57. What is a network partition?
58. Why can both sides of a partition still appear healthy locally?
59. What is the useful D00 mental model for CAP?
60. Why is "choose any two forever" misleading?
61. What is failure detection in a distributed system?
62. Why is failure detection based on inference?
63. What can a missed heartbeat mean besides permanent failure?
64. What is split-brain at a high level?

## Part H — Leaders, Consensus, Quorum

65. What is leader election?
66. Why can a system need a leader?
67. What is consensus at a high level?
68. What is quorum?
69. Why are leader election, quorum, and consensus not interchangeable?
70. What is fencing trying to prevent?

## Part I — Queues and Backpressure

71. Why do queues exist?
72. How do queues decouple producers from consumers?
73. What new operational problems do queues create?
74. What is queue backlog?
75. What happens when producer rate stays above consumer capacity?
76. What is backpressure?
77. Why is a queue not infinite capacity?
78. What is graceful degradation?

## Part J — Partitioning, Caching, Transactions

79. What is the difference between replication and partitioning?
80. What is sharding?
81. What is a hot partition?
82. Why can average system metrics hide a hot partition?
83. What problem does caching solve?
84. What new consistency problem does caching introduce?
85. What is a cache stampede at a high level?
86. Why are distributed transactions harder than local transactions?
87. What is compensation in a saga-style workflow?
88. Why is compensation not always a true rollback?

## Part K — Failure Domains and Observability

89. What is blast radius?
90. What is a failure domain?
91. Why must replicas be evaluated against failure domains?
92. Why can three replicas in one zone still fail together?
93. Why are correlation IDs useful?
94. What question do distributed traces help answer?
95. How do logs, metrics, and traces complement each other?
96. Why is user-visible availability an end-to-end property?

## Self-Check

Before reviewing the rubric, ask:

- Did I treat timeout as ambiguity rather than certainty?
- Did I connect retries to idempotency and amplification?
- Did I distinguish delivery guarantees from business correctness?
- Did I explain CAP specifically under partition?
- Did I connect replicas to failure domains?
- Did I explain queue backlog and backpressure?
- Did I connect observability across multiple services?
