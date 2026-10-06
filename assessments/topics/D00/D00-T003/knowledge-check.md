# D00-T003 — Knowledge Check

## Instructions

Answer without looking at the topic notes first. Use short explanations rather than one-word answers.

## Part A — Source, Runtime and Execution

1. What is source code?
2. Why can a CPU not directly execute most human-readable source files?
3. What is the role of a compiler?
4. What is the role of an interpreter/runtime?
5. Why is "compiled vs interpreted" not always a strict binary distinction?
6. What is a runtime?
7. What is machine architecture, and why can it affect executable compatibility?
8. What is the difference between source code and a running process?

## Part B — Dependencies and Packaging

9. What is a software dependency?
10. What is a transitive dependency?
11. What is the difference between a library and a framework at a high level?
12. What is a package?
13. What is versioning used for?
14. What is dependency locking intended to improve?
15. Why does a lockfile not guarantee full reproducibility?
16. Name four factors besides dependency versions that can affect build reproducibility.

## Part C — Build and Artifact

17. What is a build process?
18. What is a build tool?
19. What is an artifact?
20. What is the difference between source and artifact?
21. Why is "build once, promote the same artifact" useful?
22. What is the difference between an object file and a final executable in a native build?
23. Why should a production artifact have a clear identity/version?
24. What kinds of information can be used to identify an exact release?

## Part D — Configuration and Environments

25. What is configuration?
26. How is configuration different from code?
27. What is an environment?
28. Why can software work locally but fail in production?
29. Give five environment differences that can change runtime behavior.
30. Why can changing configuration alter application behavior without changing source code?

## Part E — Failure Stage Reasoning

31. What is a build failure?
32. What is a startup failure?
33. What is a runtime failure?
34. Why is identifying the failure stage useful before troubleshooting?
35. What does a nonzero exit status usually indicate?
36. Why should an engineer inspect the actual error before rebuilding or restarting?

## Part F — DevOps/SRE Connection

37. How do artifacts connect software engineering to CI/CD?
38. Why are dependency versions an operational concern?
39. Why is artifact identity important during incidents?
40. How can poor build/release discipline increase reliability risk?

## Self-Check

Before reviewing the rubric, ask:

- Did I explain relationships rather than memorize terms?
- Did I distinguish source, build, artifact, runtime and process?
- Did I separate build-time and runtime failures?
- Did I explain configuration and environment as operational concerns?
