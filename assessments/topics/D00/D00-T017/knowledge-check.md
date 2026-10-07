# D00-T017 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — System Foundations

1. What is a system?
2. Why are interactions more important than component count?
3. What is a system boundary?
4. Why can the chosen boundary change the explanation of a problem?
5. What is a system environment?
6. Why can external systems belong in the analysis?
7. What is a component?
8. What is a relationship between components?

## Part B — Inputs, Outputs, Flows, State

9. What is an input?
10. What is an output?
11. What is a flow?
12. Give four examples of flows in production systems.
13. What is state?
14. Why does state make system behavior depend on history?
15. What is a stock / accumulation?
16. What is a flow rate?

## Part C — Constraints, Bottlenecks, Throughput, Latency

17. What is a constraint?
18. What is a bottleneck?
19. Why can the bottleneck move after an intervention?
20. What is throughput?
21. What is latency?
22. Why can end-to-end latency be dominated by waiting rather than CPU?
23. What is capacity?
24. What is saturation?

## Part D — Queues and Accumulation

25. What benefit does a queue provide?
26. What risk does a queue introduce?
27. What happens when arrival rate exceeds processing rate?
28. Why can queue depth be misleading by itself?
29. Why can oldest-message age matter?
30. What does a growing stock imply about inflow and outflow?
31. Why can queues hide instability for some time?
32. How do queues affect latency?

## Part E — Local vs Global Optimization

33. What is local optimization?
34. What is global optimization?
35. Why can making one component faster worsen system behavior?
36. What is the critical path?
37. Why can optimizing a non-critical step fail to improve user latency?
38. Why should the whole system be re-measured after a bottleneck fix?
39. Why can increasing producer speed hurt a constrained consumer?
40. Why is “make every component faster” weak systems reasoning?

## Part F — Feedback Loops

41. What is a feedback loop?
42. What is a reinforcing loop?
43. What is a balancing loop?
44. Give an example of retry amplification.
45. Give an example of autoscaling as a balancing loop.
46. Why can a balancing loop still behave badly?
47. What is feedback quality?
48. Why does the strength of corrective action matter?

## Part G — Delays, Oscillation, Stability

49. What is a delay?
50. Why can delayed feedback create over-correction?
51. What is oscillation?
52. What is stability?
53. Why can autoscaling oscillate?
54. Why can queue drain time create misleading operator decisions?
55. What does lag mean in system behavior?
56. Why should operators wait for an intervention's effect before repeating it?

## Part H — Coupling and Hidden Dependencies

57. What is coupling?
58. What is tight coupling?
59. What is loose coupling?
60. What is hidden coupling?
61. Give four examples of shared hidden dependencies.
62. Why can hidden coupling create correlated failure?
63. What is a common-mode failure?
64. Why are two replicas not automatically independent?

## Part I — Backpressure, Retries, Autoscaling

65. What is backpressure?
66. Why must upstream systems respect backpressure?
67. Why can hidden retries defeat backpressure?
68. How can retries become system feedback?
69. Why can multiple retry layers multiply work?
70. Why is autoscaling a control loop?
71. Why does autoscaling not create instant capacity?
72. Why can scaling the wrong layer fail to improve the bottleneck?

## Part J — Cascading Failure and Emergence

73. What is emergent behavior?
74. Why is emergent behavior not “magic”?
75. What is cascading failure?
76. How can overload propagate through a dependency chain?
77. What is blast radius?
78. How can shared dependencies enlarge blast radius?
79. Why can one incident have multiple contributing conditions?
80. Why is “one root cause” often an oversimplification?

## Part K — Second-Order Effects, Leverage, Structure

81. What is a second-order effect?
82. Why can a successful intervention create a new bottleneck?
83. What is a leverage point?
84. Why can a small structural change outperform a large component upgrade?
85. What is the difference between symptom and structure?
86. What does event → pattern → structure → policy reasoning mean?
87. Why do recurring incidents suggest structural conditions?
88. Why are architecture decisions system interventions?

## Part L — Humans, SLOs, Architecture

89. Why are humans part of production systems?
90. How can organizational incentives affect system behavior?
91. Why can approval queues become system constraints?
92. Why can alert storms create operational feedback problems?
93. Why should observability expose relationships, not only component health?
94. Why can an SLO be treated as a system outcome?
95. Why should architecture changes be evaluated for side effects and trade-offs?
96. What is the strongest single idea you should retain from D00-T017?

## Self-Check

Before reviewing the rubric, ask:

- Did I choose an appropriate system boundary?
- Did I distinguish stocks from flows?
- Did I identify the active bottleneck rather than assume it?
- Did I reason about local vs global optimization?
- Did I understand reinforcing and balancing loops?
- Did I account for delay and oscillation?
- Did I treat retries and autoscaling as feedback systems?
- Did I identify hidden coupling and common failure domains?
- Did I consider second-order effects?
- Did I include humans and organizational incentives in the system?
