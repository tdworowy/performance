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
