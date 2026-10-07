# D00-T008 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. Why does IaC exist?
2. How do desired state and actual state differ?
3. How do you detect drift?
4. Why can drift remain hidden?
5. Declarative vs imperative: when can each be appropriate?
6. What does idempotence mean operationally?
7. Why is idempotence not universal?
8. Why is a plan safer than blind apply?
9. Why is a plan still not proof of safety?
10. How do you review a replacement action?
11. How do you review a delete action?
12. Why do dependency graphs matter?
13. When is an explicit dependency justified?
14. Why is Terraform state operationally important?
15. Why should you not universalize Terraform state-file behavior to all IaC?
16. What risks remain with remote state?
17. What does locking protect against?
18. What does locking not protect against?

## SRE

19. How can infrastructure drift complicate incident response?
20. Why should infrastructure changes be correlated with incidents?
21. How can a bad IaC change affect SLOs?
22. How do state boundaries influence blast radius?
23. Why should emergency manual changes be reconciled?
24. How can automation repeat damage?
25. How would you detect an IaC-caused reliability regression?
26. When would you roll forward instead of roll back?
27. Why can restore be required even if source code is reverted?
28. What evidence should an IaC pipeline retain?
29. Why should destructive changes have stronger controls?
30. How can plan/apply events improve incident analysis?

## Architect

31. How should state boundaries map to ownership boundaries?
32. When is one global state unacceptable?
33. When can many small states become harmful?
34. How do you balance module reuse with autonomy?
35. What should be standardized centrally?
36. What should product teams control?
37. How should secrets be handled across IaC workflows?
38. Which changes should policy-as-code block automatically?
39. Which changes still require human judgment?
40. How should environment separation be designed?
41. How do you manage cross-state dependencies safely?
42. How does provider lock-in influence IaC architecture?
43. How should apply permissions differ between dev and prod?
44. Why is GitOps not simply another name for IaC?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting / change reasoning
- FD-4: reliability / operational reasoning
- FD-5: architecture / organizational trade-offs

D00-T008 competency target: at least FD-3.
