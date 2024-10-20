# CHERI

## Compartmentalisation
- Problem: no single compartmentalisation level. Design tradeoffs between performance, security, complexity
- e.g. Chromium: tabs are sandboxed: lots of performance costs come out of process model
- Process model bad: different pages, TLB flushes, required to communicate via IPC primitives. **Obviously seen with compartmentalised applications**
- e.g. Chromium: overhead threshold reached => sandboxes are combined
- CHERI capability model: fine grained, in-address space memory protection model, based on **capabilities**

- Talk makes sense as high level overview, but what does it mean in practice?
	- How are things actually **isolated** from each other?
	- Good to know CHERI exists and what it is...

---
## Sources
- https://www.youtube.com/watch?v=4a1FcOReJRI

