---
layout: post
title: "Installing Thrift on OpenSolaris"
excerpt: "...is truly a nightmare. Following the standard in"
tags: 
- server
- open-solaris
- thrift
published: true
---

...is truly a nightmare. Following the standard install instructions, albeit with some tweaks, will get you nowhere on the OpenSolaris platform. There are many, many obstacles to overcome, and my unix-foo isn't nearly strong enough.

Thankfully, others have happened across the same problems. The [HyperTable][1] project, a very admirable NoSQL database, have available a [version of thrift][2] which has been tweaked to run on OpenSolaris. Using this, and a take on their [installation script][3], we can get a working version of thrift.

Here's a script with all the commands to get you started:

    #!/bin/bash

    # Common Packages
    pkg install SUNWgcc
    pkg install SUNWgmake
    pkg install SUNWcmake
    pkg install SUNWlibevent
    pkg install java-dev

    # SLF4J
    cd /usr/src
    wget http://www.slf4j.org/dist/slf4j-1.5.11.tar.gz -O- | tar zx
    mv slf4j-1.5.11 /usr/share/lib/slf4j

    # Apache Commons
    cd /usr/src
    mkdir /usr/share/lib/apache-commons
    wget http://mirror.fubra.com/ftp.apache.org/commons/lang/binaries/commons-lang-2.5-bin.tar.gz -O- | tar zx
    mv commons-lang-2.5/ /usr/share/lib/apache-commons/lang

    # Boost
    cd /usr/src
    wget http://downloads.sourceforge.net/boost/boost_1_40_0.tar.bz2 -O- | tar jx
    cd boost_1_40_0
    ./bootstrap.sh --with-libraries=filesystem,iostreams,program_options,system,thread,graph
    ./bjam install

    # Thrift
    cd /usr/src
    wget wget http://www.hypertable.org/pub/thrift-r820857-solaris.tgz -O- | tar zx
    cd thrift
    export CLASSPATH=.:/usr/share/lib/slf4j/slf4j-api-1.5.11.jar:/usr/share/lib/slf4j/slf4j-simple-1.5.11.jar:/usr/share/lib/slf4j/log4j-over-slf4j-1.5.11.jar:/usr/share/lib/slf4j/slf4j-ext-1.5.11.jar:/usr/share/lib/slf4j/slf4j-migrator-1.5.11.jar:/usr/share/lib/apache-commons/lang/commons-lang-2.5.jar
    ./configure --prefix=/usr CPPFLAGS='-D__BYTE_ORDER=__BIG_ENDIAN -DAF_LOCAL=AF_UNIX' LIBS='-lsocket'


  [1]: http://code.google.com/p/hypertable
  [2]: http://www.hypertable.org/pub/thrift-r820857-solaris.tgz
  [3]: http://code.google.com/p/hypertable/wiki/HowToBuildSolaris
