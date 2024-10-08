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
- According to docs, following **have been merged/pre-merge**
    - Stack smashing protection
    - Kernel address sanitisation
    - Position independent executables

### Sources
1. https://unikraft.org/docs/concepts/security
2. https://sites.pitt.edu/~babay/courses/cs3551/projects/SCADA_Unikernel/NCC_Group-Assessing_Unikernel_Security.pdf
3. https://github.com/orgs/unikraft/projects/32

### Stack Canaries
- https://github.com/unikraft/unikraft/tree/staging/lib/uksp
- Not a lot of code
- (As of yet) no clue what it is actually doing - codebase is quite large!!

### Heap Integrity Checks

### Address Space Layout Randomisation
- **OPEN MRs**:
    - https://github.com/unikraft/unikraft/pull/1317
    - https://github.com/unikraft/unikraft/pull/492 (marked as needed rework by author of above)
- _Eternal War in Memory_: most prominent address space randomisation technique. Good for implementation.
- "_If the payload's address in (virtual memory is not fixed, it is hard to reliably divert control flow_"

### Page Protections
- e.g. `W^X`, Internal Data Hardening, Guard Pages
- https://github.com/orgs/unikraft/projects/32?pane=issue&itemId=20186558: requires discussion (not a bad thing)
- `W^X` support in progress

### Building on FlexOS
- Need to find gap in research (more in paper)
- (Pierre) FlexOS needs a fair bit of work to make production ready
- https://github.com/orgs/unikraft/projects/32?pane=issue&itemId=20188373 - add compiler annotations to make compartmentalisation easier
    - Can't imagine adding compiler annotations is that difficult
    - Could build in a basic compartmentalisation system
        - Either build on FlexOS or do from scratch (depends on the quality of FlexOS)
        - Idea would be to build a very basic skeleton that others can build on with different compiler annotations

### Security-Hardened Memory Allocator
- https://github.com/orgs/unikraft/projects/32?pane=issue&itemId=19064600
- "randomisations, heap block splits"
- Will be lots of exsiting code
    - Can spend time on performance optimisation + testing
    - Conceptually will be well researched


