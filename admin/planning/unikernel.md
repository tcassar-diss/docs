
---
# Unikernels

Specialised lightweight OSs, intended to only be used within a VM
Lightweight => single hypervisor can support 100(0)s of VMs

Not meant to be run on hardware thus no driver support
Engineered for a single application - not multi-user or not multi-process. 

Very little code
* Improved security as reduced attack surface
* Fast boot times

Unikernels generate a single runtime environment, facilitating applications built for that environment. AS MINIMAL AS POSSIBLE.

Unikernels have many of the same advantages of containers, but (supposedly) are more secure than containers

---
## Unikraft Project

**Tool to make building Unikernels easier**
* Small, modular libraries which each provide a small amount of functionality
* Can be combined to end up with a unikernel specific to application needs

---
## Questions for Pierre

**About Unikernels**
1. Are unikernels meant to be ephemeral (like containers)?

**About the project**
1. Limited in scope to contributing just to `unikraft/unikraft` or forks fair game?
2. Real Time
	1. Would adding real-time features to unikraft be a viable project - noticed as of yet nothing
	2. Too large in scope? => something like real-time scheduling algorithm implementations that could be added? Is real-time even possible if unikernels run on hypervisor?
3. Saw serverless project last year (can no longer seem to be able to access the list so I'm not sure if this is already done)
	1. System to try to generate per-function unikernels automatically? Would be quite interesting
	2. Unikraft aim is to simplify development of unikernals - contribute library to auto-generate from header files/src code/something else?

**General**
1. What will the project process look like
2. What do you think separates a good project from an average one (i.e. what is needed for a good mark)
3. What is exciting and new in the unikernel space that I can look into more

Pierre website and papers with student.

---
## References

1. https://en.wikipedia.org/wiki/Unikernel#:~:text=Unikernels%20are%20built%20with%20a,the%20guest%20of%20a%20hypervisor
2. http://unikernel.org/