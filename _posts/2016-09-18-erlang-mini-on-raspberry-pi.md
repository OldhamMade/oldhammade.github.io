---
layout: post
title: Erlang-mini on Raspberry Pi
excerpt: "Install a minimal version of erlang on your small device"
category: tip
tags:
  - Erlang
  - Raspberry Pi
  - Jessie
---
[Erlang Solutions](http://erlang-solutions.com) provide a minimal version of the Erlang packages
designed specifically with embedded devices in mind (no GUI related dependencies etc), 
which weighs in under 20 megabytes).

To install, edit your `/etc/apt/sources.list` file and add the following (for Raspberry Pi[^1]):

    deb http://packages.erlang-solutions.com/debian jessie contrib
    
Import the Erlang Solutions public key:

    wget http://packages.erlang-solutions.com/debian/erlang_solutions.asc
    sudo apt-key add erlang_solutions.asc && rm erlang_solutions.asc
    
Update the package database:

    sudo apt-get update
    
Install erlang-mini:

    sudo apt-get install erlang-mini

Unfortunately, these steps didn't work for me, with the install throwing the following error:

    The following packages have unmet dependencies:
      erlang-mini : Depends: erlang-handbook but it is not installable
      
If you're presented with this error, there's a simple workaround; you can achieve the
same minimal build with the following command:

    sudo apt-get install erlang-base erlang-dev erlang-crypto erlang-parsetools erlang-ssh erlang-ssl
    
Once installed, executing `erl` should give you something like the following:

    $ erl
    Erlang/OTP 18 [erts-7.3] [source] [smp:4:4] [async-threads:10] [kernel-poll:false]

    Eshell V7.3  (abort with ^G)
    1>
    
And you're done!

***

[^1] The package is also for the Parallella; add 
`deb http://packages.erlang-solutions.com/debian oneiric contrib` to your 
`/etc/apt/sources.list` file.
