# D00-T011 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What makes a system distributed?
2. Why is partial failure fundamental?
3. Why is timeout an ambiguous signal?
4. How do you decide whether retry is safe?
5. What is idempotency?
6. Why does request identity matter?
7. What causes retry amplification?
8. Why should retry ownership be explicit?
9. What is the difference between backoff and jitter?
10. What problem does a circuit breaker solve?
11. What problem does a bulkhead solve?
12. Why can at-least-once delivery produce duplicate effects?
13. Why are ordering guarantees scoped?
14. What is replication lag?
15. What makes a stale read acceptable or unacceptable?
16. What is the correct CAP mental model?
17. Why is failure detection uncertain?
18. Why can replica count mislead you?

## SRE

19. How would you recognize retry amplification in telemetry?
20. What metrics show a queue is falling behind?
21. How can a timeout policy create cascading failure?
22. When should traffic be shed instead of queued?
23. How do hot partitions appear operationally?
24. How would you diagnose stale reads?
25. How would you identify one failing dependency in a deep request chain?
26. Why should retries be measured separately from original traffic?
27. How do failure domains affect availability?
28. How can graceful degradation protect an SLO?
29. Why must observability cross service boundaries?
30. What signals distinguish backlog from dependency latency?

## Architect

31. When should a system be distributed at all?
32. Which operations require stronger consistency?
33. Which operations can tolerate stale reads?
34. Where should idempotency keys be generated and enforced?
35. Which layer should own retries?
36. How should retry budgets be designed?
37. How should replicas be placed across failure domains?
38. When should work be synchronous vs asynchronous?
39. How should queue capacity and backpressure be designed?
40. How should hot tenants or hot partitions be isolated?
41. Where can graceful degradation be safely introduced?
42. How should exactly-once business effects be designed?
43. What coordination requires consensus or quorum?
44. How should cross-service observability be designed?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / runtime reasoning
- FD-4: reliability / recovery reasoning
- FD-5: architecture / distributed-systems trade-offs

D00-T011 competency target: at least FD-3.
