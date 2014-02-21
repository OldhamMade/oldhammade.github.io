---
layout: post
title: "Installing thrift"
excerpt: ""
tags:
  - development
  - thrift
published: true
---

I've always found thrift to be a pain to install, since there are some undocumented dependencies. The following should get thrift installed and working on CentOS5 with the minimum of fuss.

    ~# yum install build-essential gcc-c++ bison flex automake libtool \
    boost-devel libevent-devel zlib-devel
    ~# svn co http://svn.apache.org/repos/asf/incubator/thrift/trunk thrift
    ~# cd thrift
    ~# ./bootstrap.sh
    ~# ./configure
    ~# make
    ~# make install

This assumes thrift can find the python and javac binaries. If you're getting errors regarding java you're probably running the JRE rather than the JDK; install the latter and thrift should continue without fault.
