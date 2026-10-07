# D00-T016 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is automation?
2. Why is automation more than scripting?
3. What makes a good automation candidate?
4. What is current vs desired state?
5. What is reconciliation?
6. What is a control loop?
7. Imperative vs declarative automation?
8. What is a precondition?
9. What is a postcondition?
10. Why is validation required after execution?
11. Repeatability vs idempotency?
12. Why does idempotency matter for retries?
13. When should a retry not happen?
14. What are backoff and jitter for?
15. Why does timeout need a budget?
16. What is partial failure?
17. Rollback vs roll-forward?
18. What is compensation?

## SRE / Platform Engineer

19. What toil should be automated first?
20. How should auto-remediation be bounded?
21. How can automation amplify an outage?
22. What stop conditions are essential?
23. How do you handle duplicate events?
24. How do you validate unknown outcomes?
25. How should retries respect dependency health?
26. How should automation be observed?
27. What must be audited?
28. How should emergency automation differ from routine automation?
29. When should a human approve the next action?
30. What automation gaps should block production readiness?

## Architect

31. Where should desired state live?
32. How should concurrent automation be coordinated?
33. When should the platform use push vs pull?
34. Which actions should be declarative vs imperative?
35. How should global retry budgets be governed?
36. How should blast-radius limits be standardized?
37. How should automation identities be scoped?
38. Where should human approvals exist?
39. How should workflow state be stored?
40. What should happen when rollback is impossible?
41. How should policy-driven automation be designed?
42. How should self-healing authority be limited?
43. How should automation cost be evaluated?
44. How should AI-assisted automation authority change with risk?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: operational / troubleshooting reasoning
- FD-4: SRE / platform automation reasoning
- FD-5: architecture / governance / autonomy trade-offs

D00-T016 competency target: at least FD-3.
