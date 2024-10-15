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

### Questions for Pierre
- Fuzzing for evaluating security? Is it done? Alternatives for a more "robust" approach?

