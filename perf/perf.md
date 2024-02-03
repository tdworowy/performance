-1: Allow use of (almost) all events by all users
      Ignore mlock limit after perf_event_mlock_kb without CAP_IPC_LOCK  
\>= 0: Disallow raw and ftrace function tracepoint access  
\>= 1: Disallow CPU event access  
\>= 2: Disallow kernel profiling
``` bash
sudo sysctl -w kernel.perf_event_paranoid=-1
```

Sample any porogram runing on CPU at 99 Hertz for 30 s
``` bash
perf record -F 99 -a -- sleep 30 
perf report --stdio
```

trace
``` bash
perf trace -p $(pgrep mysqld)
```

list all known events
``` bash
perf list
```

list sched tracepoints
``` bash
perf list 'sched:*'
```

list events witch "block" in names
``` bash
perf list block
```

list available dynamic probes
``` bash
perf probe -l
```

show PMC statistic for command
``` bash
perf stat <command>
```

show PMC statistic for PID
``` bash
perf stat -p PID
```

show PMC statistic for entire system
``` bash
perf stat -a
```

show CPU last level cache (LLC) statistics for command
``` bash
perf stat -e LLC-loads,LLC-loed-misses,LLC-stores,LLC-prefatches <command>
```

count unhalted core cycles using a PMC raw specification (Intel)
``` bash
perf stat -e r003c -a sleep 5
```

count front-end stalls using a verbouse PMC raw specification (Intel)  
``` bash
perf stat -e  cpu/event=0x0e,umask0x01,inv,cmask=0x01 -a sleep 5
```

count syscalls per second system-wide
``` bash
perf stat -e  raw_syscalls:sys_enter -I 1000 -a
```

count syscalls by type for the specified PID
``` bash
perf stat -e  'syscalls:sys_enter_*' -p PID
```

count block device I/O events for the entire system
``` bash
perf stat -e  'block:*' -a sleep 10
```

sample CPU stack traces (via frame pointers)
``` bash
perf record -F 99 -a -g -- sleep 10 
```

sample CPU stack traces for the PID, using dwarf(debuginfo)
to unwind stacls
``` bash
perf record -F 99 -p PID --cell-graph dwarf sleep 10
```

sample CPU stack traces for a container by 
its /sys/fs/cgroup/pref_event cgroup
``` bash
perf record -F 99 -e cpu-clock --cgroup=docker/1d5..etc..
-a sleep 10 
```

sample CPU stack traces for entire system, using last
branch record (LBR;Intel)
``` bash
perf record -F 99 -a --cell-graph ibr sleep 10
```

sample CPU stack traces, onece every 100 last-level cache misses
``` bash
perf record -e LLC-load-misses -c 100 -ag sleep 5
```

sample on-CPU user instructions precisely (e.g, using Intel PEBS)
``` bash
perf record -e cycles:up -a sleep 5
```

sample CPUs at 49 Hertz, and show top process names 
and segments
``` bash
perf top -F 49 -ns comm,dso
``` 



