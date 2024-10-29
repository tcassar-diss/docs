# Minutes with Pierre

---
## 01/10/2024
- Decide on project by 15/10/2024 => will be in a good place
- Will provide VM
- Resched. next week to 1500

---
## 08/10/2024
- About the report...
- (diff between libOS and unikernel)
- Read the ComFuzz(?) paper

- Eval early good idea: drive project
- Apply flexos to a small library: 1wk
    - need to: create the boundary, identify the data that is shared
    - flexos limitations: 
        - flexos pre-compartmentalises application 
        - metrics for compartmentalisation: estimate 'security' of solution (even pre-compartmentalisation)

- Read intro, backgd, ..., ~~eval~~ for papers

- Security mem allocator: `snmalloc`

- Call with unikraft people: 
    - Priority item (e.g. not on security board) - call in 2 weeks or so

- Have a look at `virtiofs`

- Report: think about ~T-1month.
    - **Very** detailed outline (para by para) (cannot see the whole project arbitration wise)

---
## 14/10/2024
- Look at other avenues
    - Loop: dynamic analysis for compatability
     
- Reproducing what exists never as interesting

- Dynamic mem allocator problem
    - temporal safety: can leak info between compartments
    - flexos atm: each compartment gets an allocator
    - how to make a more secure version: could be very interesting
    - would be able to merge into uk? or flexos?

- Read Cambridge paper: hard to read

- Top and tail each paper

- Look at confuzz: fuzzing sounds very interesting. Can definitely use if do anything w compartmentalisation
    - LibFuzzer
    - Syzkaller

---
## 21/10/2024

- Other things vs servers that have "phase-like" application
- Bonus part of sysfinder: fine-grained

- take `strace`, run some programs, try to segregate where each syscall originates (instruction pointer)
- Split by lib: find where each library is loaded (use dynamic executable)
- (pierre) lots of syscalls from libc

- Difficult to do something to an already compartmentalised library: not many examples of already compartmentalised applications (ssh, some research samples)
- Better to take regular applications and say "assume its compartmentalised"
- Want to avoid _actually compartmentalising_ something: lots of effort, not much reward 

- Stats about per-library number/type of syscall
    - idea about phases: temporal filtering rules
    - compartments: spacial [CHECK TO SEE IF IT HAS BEEN DONE]
    - how does the kernel support this? 

- Look at traces of syscalls
    - some sequences of syscalls that make sense, some that dont
    - the idea behind the automaton in sysfinder
    
- Look at related works in sysfinder
    - Reason about how these things can be applied to compartments

- Look into other ways of filtering other than `seccomp`
    - Could look at windows
    - Userspace advanced policy enforcement


---
## 29/10/2024

- [ ] Source code analysis: source is tricky, binary restricts to a specific instruction set
    - Worth looking at building on something like LLVM IR? Or just adding unecessary complexity...

- [ ] Spent a lot of time trying to figure out how to assign a syscall to a library
    - [ ] ipynb
    - [ ] `ltrace` and `strace`: combinations, `ltrace -S`. Need to spend more time on this, definitely useful for end result of project

- [ ] Investigated different ways to filter vs `seccomp-BPF`
    - [ ] eBPF: more sophisticated filters which can be swapped out at run time
        - Presents some security challenges, TOCTOU attacks (while syscall pointers are being dereference), need more investigation
        - safe, good for observability
        - this technology is not available in Unikraft: how to port some of this to Unikraft?
    - [ ] SELinux, AppArmour (brief research)
         - difficult to config.

- `/proc/map` : shows which shared object is located in address space
    - only know at runtime, changes with ASLR
    - disable ASLR: double check that it doesn't change across two subsq. executions
- What is the best way to get a good snapshot of address space when you launch an application
    - each time a library is loaded, you need to know where it is
    - uk very modular: they have microlibaries
    - `per` microlibrary filtering policies


- different per-compartmentalisation strategies
    - how to show it makes things better
         - see how long program spends in each libary
         - 100% spends n/x with s1 syscalls filters
         - ow. i% spends n'/x with si filtered

- per-lib might require drop/increase privileges
     - eBPF: look more...
     - show that we have thought about everything, and make a series of assumptions
     - Assume that there is some form of isolation that doesn't reintroduce the overhead of systemcall: cite PhD student paper
     - ... orthoganal to our work
     - at minimum need list of assumptions

- Basic seccomp filtering in Unikraft
    - Good starting point
    - User/kernel space border is more blurry (given its a fn call in unikraft (deployment specific))
    - Even if manual hook, probably doable

- Could build very fast strace
     - linux, relies on seccomp
     - strace costly as syscalls costly: slowdown is high, use direct hooks

- both (above) requires instrumentation of syscall mechanism
    - log, filter, whatever: both similar enough
    - could add monitor, check application behaving correctly (sequences of syscalls)

- [ ] Investigated other ways of filtering an app
    - [ ] Temporal: servers, read the papers
    - [ ] C2C (configuration-to-code)
        - Debloating techniques (e.g. DCE) often configuration agnostic
        - For an app like nginx with a massive configuration space, this can lead to an unecessarily large attack surface
        - (not transparent) user provides config options (less trivial than it sounds) and _list of struct types that store the active configuration values in the application code_ (not entirely sure what that entails)
        - Also uses `seccomp-BPF`

- Docker doesn't give overhead?
     - Watch Liz Rice container talk: need to understand containerisation more deeply
     - Get some books...
     - Add to deliverables

- Synthetic load for when I figure out getting syscalls broken up by librarires
    - Benchmark?
    - Want some method of testing error path (if go with dynamic)
    - Could use dynamic, perf. evaluation (somehow) vs sysfinder: go from there.
    - Mostly worried about missing error paths, especially for "estimating security" - corner cases important

- Experiments should be defined s.th. one **single dockerfile** describes a **single experiment**
    - UnixBench, LMBench : micro benchmarks which stress OS

- hooking mechanism
    - start to look at unikraft code
    - find where border between user and kernel space is
    - mode of exec where kernel/user seperate is BINARY COMPATABILITY
        - finding syscall handler (asm entry point) set by cpu at boot time
            - "every time there is a syscall, jump here => jump to c function)"
            - c syscall handler to hook
    - more complicated where compiled together
    - want to hook between libc and kernel
    - will probably require manual hooking : <100% coverage
    - if you manage to build a quick and easy way to analyse which libraries make which syscalls

