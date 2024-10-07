# Virtualisation
- Allows multiple OSs to run on the **same hardware** without any knowledge of any other OS.
- Can be done with a **hypervisor**:
	- Virtualises the underlying hardware
	- Manages access to real hardware (either through host OS or directly)
	- Virtualisation: VMs or containers

---
## VMs and Hypervisors

- VM is an **abstraction over hardware** over which an operating system is run.
- OS thinks that it is **alone on the system** and **completely controls the hardware on which it is run**.
- VMs rely on hypervisors. There are two categories of hypervisors:
	- **Type I** hypervisors run on bare metal. Has direct access to host OS, and controls all OSs running on the hardware. Guest OSs have access to physical hardware, arbitrated by hypervisor. e.g. *KVM*
	- **Type II** a.k.a. **hosted hypervisors** only provides hardware access through host OS. Hardware access is emulated via software. e.g. *Virtual Box*

Unikraft is run as a VM over QEMU-KVM, or Xen. Acts **directly on hardware**.

---
