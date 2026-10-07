# D00-T010 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Prefer concise explanations over one-word answers.

## Part A — Container Foundations

1. Why do containers exist?
2. What deployment problem do containers reduce?
3. What is a container?
4. Why is a container not a complete virtual machine?
5. What is an image?
6. What is the difference between an image and a container?
7. How can one image create many containers?
8. Why is a container image commonly treated as a delivery artifact?

## Part B — Images, Registries, Layers, Identity

9. What is a container registry?
10. Why does a runtime need a registry?
11. What is an image tag?
12. What is an image digest?
13. Why is a digest stronger production evidence than a mutable tag?
14. What are image layers?
15. What benefits can layered images provide?
16. What risks or complexity can layers introduce?
17. What is the writable container layer?
18. Why should writable container state not be assumed durable?

## Part C — Runtime and Host Boundary

19. What does a container runtime do?
20. What does the host operating system still provide?
21. Why do containers remain dependent on the host kernel?
22. How can one host failure affect many containers?
23. Why is "container = lightweight VM" an incomplete mental model?
24. What is the main architectural difference between a VM and a mainstream Linux container?
25. Why does the host remain part of container troubleshooting?

## Part D — Isolation and Resource Governance

26. What do namespaces isolate at a high level?
27. What do cgroups control at a high level?
28. Why is process isolation different from resource governance?
29. Why should cgroup behavior stay conceptual at D00?
30. What is a resource request at a mental-model level?
31. What is a resource limit at a mental-model level?
32. Why must request/limit behavior not be overgeneralized across resources/platforms?
33. How can one workload create resource contention for others?

## Part E — Data and Storage

34. What is ephemeral data?
35. What is persistent data?
36. Why can container recreation destroy local writable state?
37. Why should durable state usually live outside the replaceable container lifecycle?
38. What is the relationship between workload lifecycle and storage lifecycle?
39. Why does persistent storage require independent recovery reasoning?
40. Why is a customer upload stored only in a container writable layer risky?

## Part F — Networking, Ports, Configuration, Secrets

41. Why do containers need networking?
42. What does an application port represent?
43. Why might container instance addresses change?
44. Why should clients avoid depending on individual instance addresses?
45. Why should configuration be externalized from the image where appropriate?
46. Why should secrets not be baked casually into images?
47. Give three examples of container runtime configuration.
48. Give three examples of secrets.

## Part G — Health and Restart

49. What question does startup health answer?
50. What question does liveness answer?
51. What question does readiness answer?
52. Why are startup, liveness, and readiness not interchangeable?
53. Why can a process be alive but the service still be unavailable?
54. What can restart automation recover from?
55. Why is restart not root-cause resolution?
56. What is a restart loop?
57. Why should repeated restart be treated as evidence?

## Part H — Orchestration Foundations

58. Why does orchestration exist?
59. What new problems appear when running many containers across many hosts?
60. What is desired state?
61. What is observed/current state?
62. What is reconciliation?
63. Why is reconciliation a loop rather than a one-time command?
64. What is a controller at a mental-model level?
65. What does the control plane do at a high level?
66. What is a node?

## Part I — Scheduling and Placement

67. What does a scheduler do?
68. Why is scheduling a matching problem?
69. What inputs may influence placement?
70. Why does free CPU alone not make a node suitable?
71. What happens if no node satisfies workload requirements?
72. Why can an orchestrator not self-heal without available capacity?
73. Why should workload placement consider failure domains?

## Part J — Service Discovery, Load Balancing, Scaling

74. Why does service discovery exist?
75. What does a stable service abstraction provide?
76. Why should only ready replicas receive traffic?
77. What is horizontal scaling?
78. What is vertical scaling?
79. Why can scaling one tier expose a downstream bottleneck?
80. What is load balancing trying to achieve?

## Part K — Updates, State, Failure, Recovery

81. What is a rolling update?
82. Why can a rolling update still fail?
83. What makes a workload stateless?
84. What makes a workload stateful?
85. Why is stateful recovery harder?
86. What is the difference between container failure and node failure?
87. Why does node failure usually have larger blast radius?
88. What is rescheduling?
89. What dependencies can block rescheduling/recovery?
90. Why does replica count alone not guarantee availability?

## Part L — Observability, Security, Platform Boundaries

91. Why should logs/metrics/events survive workload replacement?
92. Why are ephemeral workloads challenging for troubleshooting?
93. Why are containers not automatically secure?
94. What does image trust/provenance help answer?
95. Why is Kubernetes not the container runtime?
96. How do CI/CD, IaC, and orchestration differ in responsibility?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish image, container, runtime, host, and orchestrator?
- Did I explain ephemeral vs persistent state?
- Did I distinguish startup/liveness/readiness?
- Did I explain desired state and reconciliation?
- Did I explain scheduler/capacity limits?
- Did I explain service discovery and changing instance identity?
- Did I explain stateless vs stateful recovery?
- Did I explain why self-healing is bounded?
