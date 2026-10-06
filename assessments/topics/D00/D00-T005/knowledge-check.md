# D00-T005 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Use short explanations rather than one-word answers.

## Part A — Physical and Virtual Infrastructure

1. What is physical infrastructure?
2. What is bare metal in the context used by this topic?
3. What is virtualization?
4. What is a hypervisor?
5. What is the difference between a host and a guest?
6. Why can one physical-host failure affect multiple VMs?
7. What is a vCPU?
8. Why is one vCPU not always equal to one dedicated physical core?
9. What is virtual memory from a VM perspective?
10. Why can infrastructure-level CPU or memory contention affect application behavior?

## Part B — Storage Foundations

11. What is local storage?
12. What is shared or remote storage?
13. What is block storage?
14. What is file storage?
15. What is object storage?
16. Why should block, file, and object be treated as access models rather than product names?
17. Why does a device such as /dev/sda not prove the storage is physically local?
18. Why does storage persistence matter during instance replacement?
19. What new dependency appears when compute relies on remote storage?
20. Why can shared storage become a bottleneck or shared failure point?

## Part C — Networking Foundations

21. What is an IP address?
22. What is a subnet?
23. What does routing do?
24. What is a default route?
25. What is the role of a firewall?
26. Why can a network failure look like an application failure?
27. What does a load balancer do at infrastructure level?
28. Why does load balancing not guarantee high availability?

## Part D — Failure Domains and Availability

29. What is a failure domain?
30. Give five examples of shared failure domains.
31. Why are two VMs on the same physical host weak redundancy?
32. What is a region at a high level?
33. What is a zone at a high level?
34. Why must zone/region semantics be treated as provider-specific?
35. What is redundancy?
36. What is high availability?
37. Why is redundancy not the same thing as high availability?
38. What is a single point of failure?

## Part E — Provisioning and Infrastructure Change

39. What is infrastructure provisioning?
40. What risks come from repeated manual infrastructure changes?
41. What is mutable infrastructure?
42. What is immutable infrastructure at a high level?
43. What is Infrastructure as Code?
44. What benefits does IaC provide?
45. Why does IaC not automatically guarantee correctness?
46. What is infrastructure drift?

## Part F — Capacity and Scaling

47. What is capacity?
48. What is utilization?
49. What is saturation?
50. What is headroom?
51. Why can low CPU utilization coexist with poor application performance?
52. Why is headroom important during failover?
53. What is vertical scaling?
54. What is horizontal scaling?
55. Why can horizontal scaling fail if state or dependencies are not designed for it?
56. Why must capacity planning include more than CPU?

## Part G — Cloud, Reliability, Security, and Cost

57. How does cloud change infrastructure consumption?
58. What does cloud not eliminate?
59. What is the shared-responsibility model?
60. Why do responsibility boundaries vary by service model?
61. Why is infrastructure security part of application security?
62. How can infrastructure choices affect performance?
63. How can redundancy increase cost?
64. Why should architecture decisions include cost and operational skill?

## Part H — Senior / SRE / Architect Thinking

65. Why should a senior engineer separate observed, inferred, and unknown infrastructure facts?
66. Why should an SRE reason about failure domains rather than just instance count?
67. Why should an architect start from requirements before selecting infrastructure patterns?
68. Why can a lower-layer infrastructure problem appear as an application outage?

## Self-Check

Before reviewing the rubric, ask:

- Did I distinguish physical and virtual layers?
- Did I explain storage persistence and access models correctly?
- Did I separate utilization from saturation?
- Did I reason about real failure-domain separation?
- Did I avoid assuming cloud or IaC removes operational risk?
