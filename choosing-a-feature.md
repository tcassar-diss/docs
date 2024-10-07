# Choosing a Feature

Implementing intra-kernel security features requires choosing a feature.

---
## Motivation
- Unikernels should not be viewed as a single unit of trust (_The case for Intra-Unikernel Isolation; 2020, Olivier_)
- Michaels and Dilelo: _"Features like ASLR, Write-xor-Execute, stack canaries, heap integrity checks are missing or seriously flawed"_.
- Choosing a feature to implement requires
    1. What exists in Unikraft already?
    2. What has been shown possible in research (e.g. compartmentalisation on top of FlexOS)
    3. Deployment blast radius: would prefer something more widely used vs something that depends on specific hardware primitives e.g. CHERI
    4. Research 3-5 possibilities, write up MVP, talk to Unikraft maintainers.


---
## Selection Criteria
1. Performance
    1. List of metrics and acceptable slowdowns (expressed as % of original)
    2. Metrics to **quantify** how much "more secure" the unikernel when built with security features
2. Novel to Unikraft, has precedence elsewhere
    1. The maintainers should approve of an MVP before development starts
    2. The technology should be supported by research: look at codebases which implement these features


---
## Ideas

- Looking at SoK: Eternal War in Memory paper, _Currently Used Protections and Real World Protection_
- Compare each idea to the selection criteria, disqualifying as needed
- New ideas should be enqueued

### Stack Canaries

### Heap Integrity Checks

### Address Space Layout Randomisation

### Write-xor-Execute

### Building on FlexOS
- Need to find gap in research (more in paper)

