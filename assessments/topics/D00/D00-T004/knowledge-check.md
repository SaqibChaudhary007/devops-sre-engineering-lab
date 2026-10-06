# D00-T004 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Use short explanations rather than one-word answers.

## Part A — Core Architecture Concepts

1. What is application architecture?
2. What is a client?
3. What is a server?
4. Why are client and server considered roles rather than fixed identities?
5. What is a request/response interaction?
6. What is the difference between frontend and backend?
7. What is three-tier architecture?
8. Why can separating presentation, logic and data responsibilities be useful?

## Part B — Monolith and Microservices

9. What is a monolith?
10. What is a modular monolith?
11. What is a microservice?
12. Name three advantages a monolith can have.
13. Name four operational challenges microservices introduce.
14. Why is "microservices are more scalable" an incomplete statement?
15. Why can a modular monolith be a strong design?
16. What should drive the choice between monolith and microservices?

## Part C — APIs and Communication

17. What is an API?
18. What is an API contract?
19. Why is an API more than an endpoint URL?
20. What is synchronous communication?
21. What is asynchronous communication?
22. How can a slow synchronous dependency affect an upstream service?
23. What benefits can asynchronous messaging provide?
24. What new operational concerns does asynchronous communication introduce?

## Part D — State and Scaling

25. What does stateless mean for an application instance?
26. Why does statelessness often make horizontal scaling easier?
27. Does stateless mean the system has no persistent data? Explain.
28. What is a stateful application/component?
29. Why can local session state create load-balancing problems?
30. What trade-off appears when state is externalized?
31. What is horizontal scaling?
32. What is vertical scaling?
33. Why can scaling the application tier fail to improve end-to-end performance?

## Part E — Data, Cache and Load Balancing

34. What role does a database/data store play?
35. What is a cache?
36. What is a cache hit?
37. What is a cache miss?
38. Name three risks introduced by caching.
39. What does a load balancer do?
40. Why does a load balancer not guarantee high availability?

## Part F — Dependencies and Failure

41. What is a service dependency?
42. What is a dependency chain?
43. What is tight coupling?
44. What is loose coupling?
45. What is a single point of failure?
46. What is failure propagation?
47. What is a cascading failure?
48. Why can an external dependency limit your service reliability?

## Part G — Senior/SRE/Architect Thinking

49. Why should a senior engineer draw the request path before troubleshooting?
50. Why should an architect start with requirements instead of technology names?

## Self-Check

Before reviewing the rubric, ask:

- Did I explain how components connect?
- Did I distinguish symptoms from causes?
- Did I reason about state and dependencies?
- Did I avoid assuming microservices are always superior?
