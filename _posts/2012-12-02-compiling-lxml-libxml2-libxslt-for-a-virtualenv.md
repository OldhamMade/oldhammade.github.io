---
layout: post
title: "Compiling lxml/libxml2/libxslt for a virtualenv"
excerpt: ""
category: blog
tags:
  - development
  - server
  - lxml
  - python
published: true
---

Sometimes you need to ensure `lxml` is using the latest `libxml2` and `libxslt` libraries. The easiest way to do this is to set up a virtualenv for your Python project and then install `lxml` with static dependencies. Here's how to do it (I'm using `virtualenvwrapper` in my examples).

    # workon myproject
    # STATIC_DEPS=true easy_install lxml

This doesn't always work. You may see an error such as:

    ...libexslt.a(exslt.o): relocation R_X86_64_32 against `a local symbol' can not be used when making a shared object; recompile with -fPIC
    ...libexslt.a: could not read symbols: Bad value
    collect2: ld returned 1 exit status
    error: Setup script exited with error: command 'cc' failed with exit status 1

... usually on a 64bit platform. To work around this, do the following:

    # easy_install cython
    # CFLAGS="$CFLAGS -fPIC" STATIC_DEPS=true easy_install lxml

If you see an error like "`lxml/etree.so: undefined symbol: gcry_check_version`" try the following command in place of the last:

    # CFLAGS="$CFLAGS -lgcrypt -fPIC" STATIC_DEPS=true easy_install lxml

This may disable some EXSLT functionality in `libxslt`, but there's a chance you didn't have that functionality anyway if you were working with an older `libxslt` binary.
