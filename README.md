# Dissertation

Notes, planning, etc. for Third Year Project.

## Installing Unikraft on Ubuntu

- Use the install script in unikraft/unikraft repo.

Presented with the error
> ... using arch=x86_64 plat=qemu E could not start and wait for QEMU process: Could not access KVM kernel module: Permission denied qemu-system-x86_64: failed to initialize kvm: Permission denied

Solution: `chmod /dev/kvm/ 666` (safe)

- Docker build fail talking about _"failed to get lock file in /var/..."_: add user to docker group s.th. `docker` doesn't need to be run with sudo
