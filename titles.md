# Title ideas

---
## Per-compartment syscall identification/filtering
> Given a `kraft.yaml`, perform analysis and write per compartment filtering rules into the unikernel executable.

- Apply principle of least privilige to each compartment of a compartmentalised application
- Automatically analyse the syscalls needed per compartment (as per SysFinder)
- Maybe: do filtering (as per SysFilter)
- Could build this on top of FlexOS

- There are established testing methodologies for each.
- Might be difficult to motivate cases where:
    - An external boundary is easy(er) to compromise, and an exploit is possible via a syscall included because of another compartment's dependency.
    - Good argument could be futureproofing? Easier to scale with other compartments without worrying about increasing attack surface anywhere near as much.

### Things to Investigate
- Is this even needed? (could this be the research question in itself?)
    - In Unikraft, there is a reduced attack surface as only OS functionality that is needed is compiled into the Unikernel.
    - Imagine an application with two compartments: A and B. If B requires the `write` syscall, can I (after compromising A) use `write` from A?
        - If so, it would make sense to want to filter unneeded syscalls on a **per-compartment basis**.

### Questions for Pierre
- General thoughts? Is this **useful** research? Or is it just an obvious next step?
- What kind of scope of project is this: I genuinely cannot comprehend whether this could take a week or a year without getting to know the codebases a bit more
- Sysfilter measures "reduction is attack surface": how would I measure something like this in this context in a rigorous way?
- What kind of my own research would I need to do to motivate this convincingly
    - Find common applications with a large attack surface (number of syscalls accessible from compromising an outward facing API?), show how significantly it can be reduced via per-compartment syscall identification
    - Not sure it would be particularly useful: syscall count alone probably isn't a strong enough metric (`execve` more useful to an attacker than `fstat`)

---
## Memory Allocator for Compartmentalised Applications
- Less immediately interesting to me


---
## Speeding up Sysfinder
- _Section 5.3_ of sysfinder: 1/3 apps failed as they timed out (over 3hrs)
- Tomorrow: look at speedup areas in Sysfinder
- MVP: get a list of syscalls out with `gofind` or whatever the project ends up being called
- Paper suggests there is speedup potential in management of shared libraries
    - Heuristic to resolve indirect jumps: complexity grows exponentially with many shared library dependencies

- The thing with shared libraries is that they are shared
    - No opportunity for central repo somewhere associating `.so` hashes with filter list?




