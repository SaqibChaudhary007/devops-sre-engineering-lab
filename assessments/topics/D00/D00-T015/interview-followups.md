# D00-T015 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What problem does security engineering solve?
2. What is an asset?
3. Threat vs vulnerability: what is the difference?
4. What is a trust boundary?
5. What is attack surface?
6. Authentication vs authorization?
7. Why can an authenticated identity still be dangerous?
8. What is least privilege?
9. Why does duration matter for access?
10. What is separation of duties?
11. What is a secret?
12. Why are hard-coded secrets risky?
13. Why are short-lived credentials useful but not automatically safe?
14. Encryption vs hashing?
15. Why does encryption not replace access control?
16. What is defense in depth?
17. Why should security monitoring exist even with prevention?
18. What does blast radius mean in security?

## SRE

19. How should emergency access be designed?
20. Which security events should be auditable?
21. How do you detect privilege misuse?
22. How should security incidents affect recovery decisions?
23. How do you restore trust after a credential issue?
24. How do least privilege and on-call operations interact?
25. What security gaps should block launch?
26. How should backup access be separated?
27. How should patching balance urgency and change risk?
28. How can security controls affect availability?
29. How should incident response preserve useful evidence?
30. How does observability support security operations?

## Architect

31. Where are the most important trust boundaries?
32. How should human and workload identity be separated?
33. How should CI/CD identity be designed?
34. How should environment access be segmented?
35. What permissions should be temporary?
36. How should secrets be governed at scale?
37. What supply-chain evidence should be required?
38. How should artifact provenance be verified conceptually?
39. How should cloud shared responsibility influence architecture?
40. What controls reduce blast radius across accounts/projects/environments?
41. How should security ownership be split across teams?
42. How should developer experience influence security architecture?
43. How should security and reliability trade-offs be reviewed?
44. How do you prevent security from becoming a collection of disconnected controls?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: operational / troubleshooting / risk reasoning
- FD-4: SRE / security operating-model reasoning
- FD-5: architecture / governance / trade-off reasoning

D00-T015 competency target: at least FD-3.
