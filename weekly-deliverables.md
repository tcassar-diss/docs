# Weekly Deliverables

Weekly deliverables start from Week 4 because that is when I decided to start tracking weekly deliverables.

## Week 4
- [x] Plan of Week 4 deliverables
- [ ] What is the **research outcome** I want. What question am I answering?

- [ ] Project areas
    - [ ] FlexOS (if there is any time left over) (lowest priority)
    - [x] Standard memory allocators work?
    - [x] Static analysis with SysFinder, Bside

- [x] Memory allocators (4 hrs)
    - [x] How do standard memory allocators work (1hr)
        - [x] Zig talk
        - [ ] Find in osv book
        - [ ] Look at libc implementation of malloc
        - [ ] Look at how memory allocations work in **Unikraft**
    - [ ] What research exists with allocators for compartmentalisation
        - [x] FlexOS approach: allocator per compartment. Not ideal.
        - Read Cornucopia paper
            - [x] Read OS Capabilities (https://www.cs.cornell.edu/courses/cs513/2005fa/L08.html0
            - [x] CHERI talk 
        - [ ] research... is there anything that you could add?
    - Get a few **research ideas**

- [ ] Sysfinder (equiv. Bside)
    - [x] Read papers (30 mins)
    - [x] Find gaps in research: is there anything that you could add?
        - [ ] Speedup by improvng `.so` heuristic
        - [ ] Per-compartment syscall analysis + filtering framework
    - [x] Clone Bside, play around with it
        - Difficult to build
        -  Very slow on a golang hello world
        ```go
        package main

        import "fmt"

        func main() {
            fmt.Println("Hello, World")
        }
        ```
    - [ ] Look at _how_ SysFilter writes filtering rules (e.g. more detail than _using `seccomp`_)


## Week 5
(Given Pierre things that this is useful)
- [ ] (Theoretically) Determine whether FlexOS already protects against this
    - [x] Not when MPK used
    - [x] (Lefeuvre's PhD) Seems like a non-problem where EPT/VM backend is used for FlexOS
- [ ] Per-compartment syxscall filtering
    - [ ] Try to compile a two-compartment application on FlexOS. Compartment A should NOT depend on `execve`, Compartment B should. Figure out how to "compromise" Compartment A and see what happens when `execve` is called.
    - [ ] How to motivate the "per-compartment" idea: principle of least privilige yes, but is the performance/maintenance overhead worth it for a unikernel which already has a reduced attack surface
        - Argue towards future scalability: can add compartments without worrying about syscall filter rules
        
