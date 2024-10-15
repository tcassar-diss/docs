
---
# Summary of Papers

A summary of introductions of papers on unikernels

---
## FlexOS

- OS safety and isolation strategies are fixed at design time
- FlexOS allows users to select strategies at build time, and has a tool to navigate search space.
- Aimed to provide...
	1. Configurable isolation granularity
	2. Configurable hardware isolation strategies
	3. Configurable software isolation strategies
	4. No performance overhead due to **felxibility**
	5. No high porting cost for existing software
	6. Tool to help user navigate design space

### New words
- _Trusted Computing Base_: combination of technologies (hardware, firmware, software, and more) that provides a **secure environment for computations**
- Source code libraries call external functions via **abstract gates**
	- What is an external function in this context?
	- Is this split between processes? If so would need to add paging to Unikraft: no more single address space. Bad.


### Designing FlexOS

### Porting applications with FlexOS
- Two things needed
	- **Call Gates** Make external function calls through "abstract gates" instead of referencing the external library directly
		- e.g. calls to `libc` for instance are made via "abstract gates"
		- Painful to do manually every time, so use `coccinelle` tool (pre-packaged with FlexOS) to rewrite to a `flexos_gate` call
		- At compile time, the `flexos_gate` call is rewritten at compile time with chosen method of isolation
		- Test that all have been done properly (see FlexOS README).
	- **Data sharing over API**: paper alludes to it being done automatically: don't believe either are fully automated unfortunately

#### Applications to Port
- [ ] Hello, world (provided)
- [ ] Redis (provided)
- [ ] tbc... maybe a standard command line tool?

### Gaps in FlexOS

- Identified by the paper
	- ~~More hardware isolation mechanism support (e.g. SGX, CHERI)~~ (already been done)
	- Support for more software hardening techniques
	- Tool to better search config space (not really what I want to be doing)


#### Problems
- FlexOS already built on top of Unikraft: what would I be adding more than just a refactor?
- Adding support for hardware isolation: nothing new there either, not big enough in scope or interesting enough
- Would prefer to build on **Unikraft** instead of FlexOS

