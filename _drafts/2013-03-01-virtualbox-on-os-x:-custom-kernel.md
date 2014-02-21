---
layout: post
title: "VirtualBox on OS X: Custom kernel"
excerpt: "yum install -y gcc rpm-build ncurses-devel cd /usr"
tags: 
- general
published: false
---

    yum install -y gcc rpm-build ncurses-devel
    cd /usr/src
    wget ftp://ftp.kernel.org/[path/to/latest/kernel].tar.bz2 -O- | tar jx
    cd linux-[version]/
    cp /boot/config-`uname -r` ./.config
    make menuconfig

1. load the config file.
1. enable "tickless system" if available
1. set the cpu timing frequency to 100hz
1. change the Preemption Model to "No Forced Preemption (Server)"
1. set the i/o scheduler to "no-op"

Then...

    make rpm
