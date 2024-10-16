# Memory Allocators

## Overview
- Stack memory
	- very fast, handled by the compiler. Fast allocation, fast cleanup. 
	- Fixed total memory, fixed sizes, fixed lifetimes.
	- Lifetime limitations mean you can't make e.g. a linked list on the stack (equiv, to use-after-free)

- Page allocator
	- `mmap`, `munmap` syscalls can request memory. (syscall slow). Not great for a langauge allocator
	- OS only deals with _pages_ so `malloc(8)` actually allocates a whole page
	- Can we cut out OS? No, as it has the memory. Can we malloc all the memory we might need when program start? No, very wasteful.
	- So... design 'smarter' allocators...

- Bump Allocator
	- Simplest allocator that we can make
	- Stores an end index.
	- Use a fixed buffer: as you allocate, you bump the end index
	- Tracks free space left and memory previously consumed
	- Very **simple**, very **fast**.
	- More control over lifetime via buffer
	- But... fixed total memory
	- Cannot free memory!! (without resetting the whole thing by pointing end pointer at beginning)
	- Bump alloc. with expandable memory
		- Create new buffers when buffers are full
		- Requires a 'backing allocator' (can use the OS). Far fewer calls to OS so faster
		- Called an **arena allocator**
		- Significantly more performant, combination of page allocator and bump allocator
		- **Still cannot free individual memory** but can free everything with some syscalls
			- Some problems don't require freeing individual memory: lots of allocations on one lifetime (e.g. a linked list)
			- Freeing a linked list of length `n` requires `n` frees: would be nicer to just wipe it all
			- Sometimes you don't need to free individual memory: okay to have some garbage => can use an arena allocator

- Freeing individual memory
	- `free(n)` call prepends size to linked list
	- `malloc(n)` calls: traverse linked list, find block of matching size and return that pointer
	- => slow malloc calls but lower memory footprint. 
	- However
		- Allocs have minimum size (at least the size of the next pointer for the LL)
		- Very slow
		- Memory fragmentation will occur - bad for cache, hard to defrag...
	- Could use size buckets...

- Size buckets
	- Different lists for different sizes, so don't have to look through entire list
	- Fragmentation limited: all allocs end up one of some fixed size behind the scene (but there is still some fragmentation)
	- More wasteful, as allocations need to have fixed sizes!
	- Leads to **cache pressure**: due to linked lists jumping around in memory

- Make memory more cache friendly: use **arrays**, **Slab allocator**
	- (similar to arena)
	- Multiple slabs s.th. each slab has the same amount of memory.
	- Means that things being logically allocated together have a good chance of being physically right next to each other
	- Allocations still have fixed sizes, but
		- No longer so slow (array vs LL)
		- No memory fragmentation
		- No more cache pressure
	- Metadata storage is wasteful... (slabs need metadata)  (don't understand this point...)

- Threading: naive way through locks, but locks are slow. So give different threads different "memory affinity"

- No such thing as a real **general purpose allocator** (hence zig has no default allocator)
- (how does keep different allocators from stepping on each others toes: rely on `mmap` and `munmap`?)


## OSV

## libc `malloc`

## Hardening

## Allocators for compartmentalisation

---
## Sources
1. https://sumofbytes.com/blog/whats-a-memory-allocator-anyway
2. https://youtu.be/vHWiDx_l4V0 (Benjamin Feng, zig mem. alloc. talk)

