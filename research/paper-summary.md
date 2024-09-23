
---
# Summary of Papers

A summary of introductions of papers on unikernels

---
## FlexOS

Novel OS to allow users to easily specialise the safety/isolation strategy of an OS at compilation/deployment time vs design time.

At the moment, OSs commit to high-level safety mechanisms at design time
* Software verification
* Hardware isolation
* Runtime checking
Not normally changed after compile time

With FlexOS user decides *at build time* what security approach(es) they need. Can therefore be done dynamically (Redis - from 80 configurations find 5 with most ideal security/performance tradeoff)

Compartments are created dynamically according to user specification. There is a massive design space though - one of the objectives is to help users navigate the design space. 