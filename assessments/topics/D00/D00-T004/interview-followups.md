# D00-T004 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is the difference between client/server roles and frontend/backend responsibilities?
2. How would you trace a user request through an unfamiliar application?
3. Why can low application CPU coexist with high user latency?
4. How can a dependency become the real bottleneck?
5. Why can horizontal scaling move rather than remove a bottleneck?
6. What does local in-memory session state do to instance replaceability?
7. What is the difference between stateful service and stateful system?
8. Why can a load balancer route traffic correctly while users still see failures?
9. How would you distinguish database latency from application latency?
10. Why is a shared database a coupling point?
11. What evidence would you collect before blaming a downstream dependency?
12. How can a cache improve latency and still create correctness problems?

## SRE

13. Which SLIs best represent user impact in a multi-tier application?
14. Why is process uptime insufficient as a service-health signal?
15. How can dependency latency consume an upstream service's SLO?
16. What should you monitor for asynchronous queue backlog?
17. Why can retries create a cascading failure?
18. How would you identify a single point of failure?
19. What does graceful degradation mean in architecture?
20. How can external dependency failure be isolated from non-critical user journeys?
21. Why should dependency-level telemetry be correlated with end-to-end latency?
22. How do state and failover interact?

## Architect

23. When is a monolith a better choice than microservices?
24. When does a modular monolith become attractive?
25. What requirements justify independent service deployment?
26. How should team structure influence service boundaries?
27. Why can too many service boundaries create excessive network coupling?
28. What are the trade-offs of synchronous versus asynchronous communication?
29. When should state be externalized?
30. What trade-offs come with a shared cache?
31. How do you decide whether to scale vertically or horizontally?
32. What does a 99.99% availability target imply for single points of failure?
33. How should external API dependency risk influence design?
34. When should an API gateway be introduced?
35. How would you design for a dependency that is slow but not completely unavailable?
36. Why should architecture decisions include cost and operational skill?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: failure/troubleshooting
- FD-4: reliability/operations
- FD-5: architecture/trade-offs

D00-T004 competency target: at least FD-3.
