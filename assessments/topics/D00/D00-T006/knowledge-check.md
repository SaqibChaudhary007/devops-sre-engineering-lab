# D00-T006 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer short explanations over one-word answers.

## Part A — Cloud Operating Model

1. What changes operationally when infrastructure is exposed through APIs?
2. Why is "cloud is someone else's computer" an incomplete definition?
3. Name the five essential NIST cloud characteristics taught in this topic.
4. What is on-demand self-service?
5. What is resource pooling?
6. What is measured service?
7. Why does faster provisioning increase governance requirements?
8. Why does cloud not eliminate infrastructure fundamentals?

## Part B — Control Plane and Data Plane

9. What is a control plane?
10. What is a data plane?
11. Give two control-plane actions.
12. Give two data-plane actions.
13. Why can a control-plane failure occur while some workloads still serve traffic?
14. Why can a healthy cloud portal coexist with an application outage?
15. Why should incident response separate management-path health from workload-path health?
16. What operational risk appears when the control plane is unavailable during a scaling event?

## Part C — Scalability, Elasticity, and Autoscaling

17. What is scalability?
18. What is elasticity?
19. How are scalability and elasticity related but different?
20. What is autoscaling?
21. What kinds of signals can drive autoscaling?
22. Why can autoscaling fail to improve user performance?
23. Why can autoscaling increase cost without improving throughput?
24. Why must downstream dependencies be considered before scaling the application tier?
25. What is an autoscaling ceiling?
26. How can quotas interfere with autoscaling?

## Part D — Regions, Zones, and Failure Domains

27. What is a region at D00 level?
28. What is an availability zone at D00 level?
29. Why are region/zone semantics provider-specific?
30. What is a cloud failure domain?
31. Why can one-zone deployment create a larger blast radius?
32. Why is multi-zone not automatically disaster recovery?
33. What additional concerns appear in multi-zone architecture?
34. What kinds of failures might require multi-region design rather than multi-zone only?

## Part E — Managed Services and Service Models

35. What is a managed service?
36. What operational responsibilities may move to the provider?
37. What responsibilities usually remain with the customer?
38. What is IaaS?
39. What is PaaS?
40. What is SaaS?
41. What does serverless abstract?
42. Why does serverless still depend on servers?
43. Why is "managed = provider handles everything" incorrect?
44. Why do responsibility boundaries vary by service type?
45. What trade-offs can managed services introduce?

## Part F — Deployment and Cloud Models

46. What is public cloud?
47. Why does public cloud not mean every resource is internet-facing?
48. What is private cloud?
49. Why is virtualization alone not the same thing as private cloud?
50. What is hybrid cloud?
51. What is multi-cloud?
52. Why is multi-cloud not one of the formal NIST SP 800-145 deployment models?
53. Why can multi-cloud increase operational complexity?
54. Why can multi-cloud fail to improve resilience?

## Part G — Resource Lifecycle and State

55. What is an ephemeral resource?
56. What is a persistent resource?
57. Why should important state not depend on a disposable compute instance?
58. What does the pets-vs-cattle metaphor try to communicate?
59. What can immutable replacement reduce?
60. Why does immutable infrastructure not eliminate the need to design state and rollback?

## Part H — Identity, Quotas, Governance, and Cost

61. What is cloud identity?
62. What is least privilege?
63. Why is broad cloud API access especially risky?
64. What are tags/metadata useful for?
65. What are quotas/service limits?
66. Why are quotas architectural constraints?
67. What is cloud metering?
68. Why does metering affect engineering decisions?
69. How can elasticity improve cost efficiency?
70. How can autoscaling create cost spikes?
71. Why is cloud cost part of architecture?
72. What is cloud governance?
73. What is policy-as-code at a high level?

## Part I — Observability, Blast Radius, Resilience

74. Why must observability handle dynamic resources?
75. What is blast radius?
76. Give four examples of blast-radius scope.
77. What is resilience?
78. How is resilience different from availability?
79. Why is backup not the same as high availability?
80. Why is multi-zone not automatically disaster recovery?
81. What does cloud-native mean at a high level?
82. Why is cloud-native broader than Kubernetes?

## Part J — Senior / SRE / Architect Thinking

83. Why should a senior engineer ask which service model is in use?
84. Why should an SRE correlate control-plane changes with incidents?
85. Why should an architect start with availability, recovery, geography, security, cost, and operational skill before choosing services?
86. Why can the "highest abstraction" service still be the wrong architecture choice?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish control plane from data plane?
- Did I distinguish scalability from elasticity?
- Did I explain shared responsibility correctly?
- Did I avoid equating serverless with no servers?
- Did I reason about quotas, cost, and blast radius?
- Did I avoid equating multi-zone with disaster recovery?
- Did I avoid equating cloud-native with Kubernetes?
