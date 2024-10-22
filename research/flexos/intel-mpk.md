# Intel Memory Protection Keys

- Memory protection directly from userspace
	- Cuts out need for `mprotect` syscall (alters page table entries)

- Tag memory pages using (previously unused) 4 bits: e.g. 16 possible distinct keys with which pages can be tagged (`libmpk` uses software to "add more" protection domains)
- (Still require syscalls to tag/free pages)
- About **who can read/write specific pages in memory**
	- Permissions per thread are stored in the `PKRU` register
	- (Q: what stops me from overwriting my PKRU register? Done via a syscall?

- Much cheaper than `mprotect`
	- `mprotect` modifies PTE => runs in linear time w.r.t. no. of PTEs; MPK pays linear time once (to tag a key), then updates are constant time.

- Vulnerable to **protection-key-use-after-free** attacks

## Architectire
- 4 bits used to generate keys
- MPK tracks r/w permissions with the Protection Key Rights Register (PKRU)
	- Provides read/write instructions to the register (kernel mode)
	- Per-core: => different threads can have different permissions
- ~20 cycles for permission change vs ~1,000 for `mprotect` syscall


## Threats against MPK-based protection
- `WRPKRU` syscall: update page permissions
- Bypass by using syscalls that ignore the `PKRU` register
- (Programmer error): exploiting unintentionally exposed memory


---
## Sources
- https://charlycst.github.io/posts/mpk/
- https://www.usenix.org/conference/atc19/presentation/park-soyeon
- https://gts3.org/assets/papers/2023/park:mpkfacts.pdf

