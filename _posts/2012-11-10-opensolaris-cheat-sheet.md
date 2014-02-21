---
layout: post
title: "OpenSolaris Cheat Sheet"
excerpt: "Some useful commands for working with OpenSolaris"
tags:
  - server
  - opensolaris
published: true
---

Some very useful commands for working with OpenSolaris:

`pfexec` - `sudo`

`prstat` - `top`

`pgrep` - find the PID of process: `pgrep cron`

`pstack` - view the call stack of a process

`pfiles` - find the files opened by a process; similar to `lsof`

`psig` - list signal actions and handlers

`man N proc` - get more information on the process *N*


`dtrace` - dynamic tracing compiler and tracing utility

`vmstat` - virtual memory statistics; use in place of `free`

`mpstat` - show running information per processor; `vmstat`-like output

`iostat` - show system/device input/output

`netstat` - show network input/output, bound ports, etc.


`modinfo` - like `lsmod`

`modload` - like `modprobe`

`modunload` - like `rmmod`

`scanpci` - scan for PCI devices

`psrinfo -v` - show info on cpus; `cat /proc/cpuinfo`

`prtconf` - show hardware info; similar to `lshw`


`beadm` - manage boot environments

`pkg` - install/remove packages (similar to `apt`, `yum`)


`svcs` - view services; like redhat's `chkconfig --list`

`svcadm` - administer services; `service S start|stop` > `svcadm enable|disable S`

`svccfg` - add or change services; like redhat's `chkconfig --add|--remove` but more powerful
