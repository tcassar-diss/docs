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
- [ ] ~~Per-compartment syxscall filtering~~
    - [ ] Try to compile a two-compartment application on FlexOS. Compartment A should NOT depend on `execve`, Compartment B should. Figure out how to "compromise" Compartment A and see what happens when `execve` is called.
    - [x] How to motivate the "per-compartment" idea: principle of least privilige yes, but is the performance/maintenance overhead worth it for a unikernel which already has a reduced attack surface
        - Argue towards future scalability: can add compartments without worrying about syscall filter rules
        

---
### Completed in Week 5

- Statistics on Syscalls per library
    - Tried to analyse some applications with `strace`: see which syscalls they used and which libraries were invoking them
    - Limitation 1: Needed some workload to run for an accurate `strace` output. Solution: use benchmarks
    - Limitation 2: `strace` only shows which syscalls are made, not where they originate from. More difficult than expected...
    - Limitation 3(?): `ltrace` seems to be reliant on _dynamic executables_. Go by default builds static executables and `ltrace` wasn't happy. 

    - (Unless I've missed something) seems like it could be an interesting project to dedicate some time to
        - Static analysis tool? Modify `sysfinder` to record which library a syscall was made from? No idea where to start in the binary src: might be easy, might be hard...
        - Can get PC value information from `ltrace`: could somehow use?

    - (Come to think of it) this is effectively my project: analyse some subset of syscalls broken down by libary

- Liz Rice: eBPF, _Chapter 8: eBPF for Security_
    - Some tools which use eBPF to gather information about the syscalls being generated
        - Inpsektor Gadget (generates profiles for containers in a k8s pod)
        - seccomp filter as an OCI runtime hook [github.com/containers/oci-seccomp-bpf-hook](https://github.com/containers/oci-seccomp-bpf-hook)
        - (what is an OCI hook? https://man.archlinux.org/man/oci-hooks.5.en something to do with containers)

    - Both dynamic analysis?? seems unsuitable for generating a seccomp filter? odd...

    - "Since eBPF programs can be loaded dynamically and can detect events triggered by preexisting processes... Users can modify the set of rules being applied without having to modify the applications or their configuration." could be very useful for compartmentalised applications
        - Would need overhead to track which compartment we are in, and have the right eBPF filter linked
        - Sounds difficult expensive and difficult)
        - Presents a **TOCTOU** issue (as kernel derefs. syscall arguments and copies into kernel space (hence seccompBPF doesn't suffer from this problem))
        - Hence, **good for observability** but not for security... Enter Sysmon for Linux (at a cost)
        - Problem with Sysmon is it needs to WAIT FOR THE SYSCALL TO FINISH so can't prevent an action from taking place
    
   - Linux Security Module: safe well-defined API that eBPF can hook into without TOCTOU vulnerability

- Interspersing traces from `strace` and `ltrace`
    - Could use PC value to try to assign a (partial?) ordering to library calls/system calls
    - Load into dataframe, use `ltrace` data to estimate in which library we are, and `strace` to assign syscalls to the library

- [ ] Need to look at ELF format
     - `.dynsym` table
     - Is there symbol information that will help identify which libraries make which syscalls?


---
- Questions to answer
    - [ ] Are there any other applications that exhibit easy spacial separation?
    - [ ] 



---
### Week 6



