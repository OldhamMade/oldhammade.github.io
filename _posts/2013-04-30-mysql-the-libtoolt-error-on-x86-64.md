---
layout: post
title: "MySQL & the libtoolT error on x86_64"
excerpt: "Quick fix for the `cannot remove 'libtoolT': No such file or directory` error"
tags:
  - server
  - mysql
published: true
---

Quick fix for the `cannot remove 'libtoolT': No such file or directory` error that can raise when trying to compile MySQL on x86_64.

After downloading, unpacking, and changing directory...

    [mysql-x.x.x]# libtoolize --force
    Using `AC_PROG_RANLIB' is rendered obsolete by `AC_PROG_LIBTOOL'
    You should update your `aclocal.m4' by running aclocal.
    [mysql-x.x.x]# aclocal
    [mysql-x.x.x]# cp BUILD/compile-pentium64 ./compile
    [mysql-x.x.x]# autoreconf

...then proceed as usual.
