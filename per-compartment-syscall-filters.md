# Per-Compartment Syscall Filtering

1. Identify a superset of syscalls that **each compartment** can make (e.g. sysfinder)
2. Automatically write in filtering rules (e.g. with `seccomp`) on a _per-compartment_ basis

Would result in
    - Ability to scale projects without worrying about increasing attack surface
    - Principle of least privilege can be applied to each compartment
    - (Likely) lower performance overheads than building with an EPT/VM backend, but more secure (via rediced attack surface) than building with CHERI/MPK

Source code
- Is compartment information easily deducible from a binary
- Access to source might be needed: problem would be supporting different languages, much more usable when only needing binary
- Maybe rely on binary + `kraft.yaml`? Or can compartments be deduced from binary? Would this be a waste of time as very specific to FlexOS?

General
- Would a more useful tool be
    - Given a binary + compartment specification, write in the filters in some "compartmentalisation agnostic" way
    - e.g. each user defined "compartment" gets its own filtering rules


Actually, this might all be useless: look at **how** sysfilter writes in filtering rules
    - Global addition would be very very naive

---
## How SysFilter actually works.
(By my reading of Section 3.1.3 of SysFilter paper)
- System call set is identified
- A single c-BPF "program" is generated and compiled as a `.so`
- At link time, it is linked to the main binary (whatever is meant by the main application binary) (presumably the one with the `main` function)
- The `.so` file contains **one function**

- ... surely cannot be more complex than a single global syscall filter

---
## Is there a way to generalise past FlexOS?

- Research: other compartmentalisation systems: is there something more applicable / an easier way to generalise?




---
## Estimation Tool  
Estimate how safe the compartmentalisation will be from a syscall perspecive
- Dynamic analysis much faster

Per compartment syscall filtering
    - where to go from there
    - to build the rule, would need static
    - 

- Maybe tool in which you can identify which compartment is most likely to be hacked


