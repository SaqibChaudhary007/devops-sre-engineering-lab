# D00-T014 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Observability Foundations

1. What is observability?
2. What is monitoring?
3. How do monitoring and observability differ?
4. Why should they not be treated as competing concepts?
5. What is telemetry?
6. What is instrumentation?
7. Why is telemetry not the same as observability?
8. Why is observability useful for unexpected system behavior?

## Part B — Metrics, Logs, Traces, Events

9. What question do metrics commonly answer?
10. What question do logs commonly answer?
11. What question do traces commonly answer?
12. What question do events commonly answer?
13. Why is no single signal sufficient for every investigation?
14. What is meant by the “three pillars” model?
15. Why is the “three pillars” model incomplete?
16. Give three other useful forms of observability context beyond metrics/logs/traces.

## Part C — Context and Correlation

17. What is telemetry context?
18. Why does context matter?
19. What is correlation?
20. What is a request ID?
21. What is a correlation/workflow ID?
22. What is a trace ID?
23. Why are these identifiers not universal synonyms?
24. What is the durable principle behind correlation identity?
25. What is a span?
26. What is trace-context propagation?

## Part D — Structured Logging

27. What is structured logging?
28. Why can free-form logs be harder to operate?
29. Name six useful structured-log fields.
30. Why can logs become noisy?
31. Why should log severity be used carefully?
32. Why should sensitive values be excluded or governed?

## Part E — Metrics, Dimensions, and Cardinality

33. What is a metric dimension/label?
34. Why do dimensions improve diagnostic context?
35. What is cardinality?
36. Why does high cardinality create cost and complexity?
37. Why is user_id risky as a metric label?
38. Why is request_id risky as a metric label?
39. Where might high-cardinality context belong instead?
40. Why should one vendor’s cardinality threshold not be treated as universal?

## Part F — Aggregation, Latency, and Distributions

41. What is aggregation?
42. How can aggregation hide local failures?
43. Why can an average latency be misleading?
44. What does p95 latency mean at a high level?
45. Why does tail latency matter?
46. Why should latency be treated as a distribution?
47. What is the D00-level lesson about histograms/distributions?
48. Why does over-segmentation also have a cost?

## Part G — Traffic, Errors, Saturation, Methods

49. What does traffic tell you?
50. What does saturation tell you?
51. Why can saturation rise before total failure?
52. What are the four golden signals?
53. What does RED stand for?
54. What does USE stand for?
55. Why are golden signals not a complete observability architecture?
56. Why are RED and USE complementary rather than interchangeable?

## Part H — Black Box, White Box, Business and Dependencies

57. What is black-box monitoring?
58. What is white-box monitoring?
59. Why are both useful?
60. What is synthetic monitoring?
61. Why can business signals detect failures technical metrics miss?
62. What dependency telemetry is useful?
63. Why is queue depth alone insufficient?
64. Why can oldest-message age be important?

## Part I — Events, Change Markers, and Time

65. What is a change marker?
66. Why should deployments appear on telemetry timelines?
67. Why is timing useful during incidents?
68. Why are clocks imperfect evidence in distributed systems?
69. Why does correlation not prove causation?
70. What should happen after a correlation creates a hypothesis?

## Part J — Sampling, Retention, Cost

71. What is sampling?
72. Why is sampling useful?
73. What evidence can sampling lose?
74. What is retention?
75. Why is longer retention not always better?
76. What cost categories exist in observability?
77. Why is “collect everything forever” weak architecture?
78. Why should signal value influence retention and sampling?

## Part K — Security, Privacy, Overhead, Blind Spots

79. Why is telemetry production data?
80. What kinds of sensitive data can appear in telemetry?
81. What controls should govern telemetry?
82. Why does instrumentation have performance overhead?
83. What is a telemetry blind spot?
84. Give four examples of missing context that can create blind spots.
85. Why are ephemeral workloads a special observability challenge?
86. Why should evidence survive the workload instance?

## Part L — Dashboards, Alerts, Troubleshooting, Architecture

87. What should a good dashboard answer?
88. Why is panel count not observability maturity?
89. What makes alert context useful?
90. What does evidence-first troubleshooting mean?
91. Why should troubleshooting start with impact and scope?
92. Why are random commands a weak starting point?
93. How do metrics, logs, and traces support hypothesis validation?
94. How should recovery be validated with telemetry?
95. What makes an observability architecture mature?
96. What is the strongest single idea you should retain from D00-T014?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish observability from monitoring and telemetry?
- Did I explain metrics/logs/traces/events correctly?
- Did I understand context and correlation identity?
- Did I explain cardinality risk?
- Did I explain average vs tail latency?
- Did I understand sampling/retention/cost trade-offs?
- Did I explain correlation vs causation?
- Did I start troubleshooting from user impact and evidence?
