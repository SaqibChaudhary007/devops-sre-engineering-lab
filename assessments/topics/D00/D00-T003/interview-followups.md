# D00-T003 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is the difference between source code and an artifact?
2. Why can a build succeed but an application fail at startup?
3. Why can startup succeed but runtime still fail later?
4. What is the difference between build-time and runtime dependencies?
5. Why can dependency version drift create production differences?
6. What does a lockfile solve, and what does it not solve?
7. Why is exact artifact identity important during troubleshooting?
8. What is the difference between code and configuration?
9. Why is "works on my machine" usually an environment problem statement, not a root cause?
10. How would you prove QA and production are using the same artifact?
11. Why can architecture compatibility matter for native binaries?
12. When would rebuilding be the wrong first response?

## SRE

13. How can build/release quality affect SLOs?
14. Why should deployment events be visible in observability systems?
15. Why is release identity useful when correlating an incident with change?
16. How can an unpinned dependency increase reliability risk?
17. Why should startup failures produce explicit logs and nonzero exit codes?
18. What should an SRE know about the exact runtime version in production?
19. How can configuration drift create availability incidents?
20. Why is rollback safer when artifacts are immutable and versioned?
21. How can release automation reduce operational toil?
22. What signals would help distinguish bad code from bad environment/configuration?

## Architect

23. How do language/runtime choices affect operations?
24. Why might a team choose native binaries versus runtime-dependent applications?
25. What are the trade-offs of static versus dynamic dependencies at a high level?
26. Why should dependency lifecycle/supportability influence architecture?
27. How should artifact strategy affect multi-environment deployment?
28. Why does supply-chain provenance matter?
29. When can "build once, promote" be difficult to apply?
30. How would you design a platform so application teams cannot silently deploy untraceable artifacts?
31. What trade-offs exist between flexibility and reproducibility?
32. How can container images improve consistency while still leaving external environment dependencies?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: failure/troubleshooting
- FD-4: reliability/operations
- FD-5: architecture/trade-offs

D00-T003 competency target: at least FD-3.
