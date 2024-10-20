# Filtering Syscalls with `seccomp`

- Attackers can do bad things with syscalls: filter unexpected syscalls => reduce attack surface

- Mechanism within kernel to allow syscalls to be 
	- logged
	- blocked

- `libseccomp`: user level library: exposes nice API

- `seccomp` hit can kill an erratic process

- seccomp for dynamic analysis: identifying syscalls. Run with blank filter, allow all + log
	- how does this hit every state? insane...

- `strace` can be used to generate list of syscalls as well

- Ideally...
	- parent sets up strace filtering
	- child runs, unaware of syscall filtering

- Need to look at `init` process and `systemd`...



