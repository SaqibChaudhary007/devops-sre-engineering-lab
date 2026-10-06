# D00-T005 — Senior / SRE / Architect Follow-Ups

## Senior Engineer

1. What is the practical difference between a physical host and a VM guest?
2. How would you determine whether a Linux system appears virtualized?
3. Why should you not infer physical topology from guest-visible devices alone?
4. How do you distinguish local storage from persistent remote storage operationally?
5. Why can storage latency appear as application slowness?
6. How can a route problem appear as a service outage?
7. Why can a VM be healthy while the service is unavailable?
8. What evidence proves two VMs are in independent failure domains?
9. Why does low CPU not prove sufficient capacity?
10. What is the difference between utilization and saturation?
11. How do you estimate whether failover headroom is sufficient?
12. What kinds of infrastructure drift can manual changes create?
13. When can mutable infrastructure be reasonable?
14. What operational benefit can immutable replacement provide?

## SRE

15. How do failure domains affect SLO risk?
16. What signals would you monitor for compute saturation?
17. What signals would you monitor for storage saturation?
18. What signals would you monitor for network saturation?
19. Why is redundancy across one host not enough?
20. How would you test failover capacity safely?
21. How can shared storage undermine application redundancy?
22. Why can multiple healthy guests still fail together?
23. How do recovery time and capacity reserve interact?
24. What should be observable about infrastructure placement?
25. How does infrastructure change correlate with incidents?
26. Why should availability be evaluated end to end rather than component by component?

## Architect

27. When would bare metal be preferable to VMs?
28. When would virtualization provide the better trade-off?
29. How do block, file, and object storage choices affect application design?
30. What requirements justify multi-zone deployment?
31. When would multi-region deployment be justified?
32. Why does greater redundancy increase cost and complexity?
33. How should stateful dependencies influence HA design?
34. How do you decide between vertical and horizontal scaling?
35. How should compliance/geography affect region selection?
36. How should team skill affect self-managed vs managed infrastructure choices?
37. What trade-offs exist between mutable and immutable infrastructure?
38. How does IaC change governance and review?
39. Why should shared-responsibility boundaries influence security architecture?
40. How do you avoid over-engineering infrastructure for a small workload?

## Follow-Up Depth

- FD-1: definition
- FD-2: explanation
- FD-3: troubleshooting/failure reasoning
- FD-4: reliability/operations
- FD-5: architecture/trade-offs

D00-T005 competency target: at least FD-3.
