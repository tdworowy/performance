```bash
bpftrace -e 't:syscalls:sys_enter_kill{time("%H:%M:%S "); printf("%s (PID %d) send a SIG %d to PID %d\n", comm, pid, args->sig, args->pid);}'
```

```bash
bpftrace -e 't:syscalls:sys_enter_recvfrom { @ts[tid] = nsecs; } t:syscalls:sys_exit_recvfrom /@ts[tid]/{ @usces = hist((nsecs - @ts[tid]) / 1000); delete(@ts[tid]);}'
```