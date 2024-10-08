# KASLR in the Age of Micro-VMs

https://dl.acm.org/doi/10.1145/3492321.3519578

## Overview
- Modern kernels do KASLR inefficiently in bootstrapping.
- Cloud people (e.g. AWS) want fast boot times, so they scrap bootstrapping steps e.g. KASLR.
- **In-monitor** ASLR: the vmm implements KASLR for the guest kernel.
- 22% faster than bootstrapping KASLR, 4% slower than running with none.
- No modification of guest kernel (researchers used Linux).

