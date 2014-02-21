---
layout: post
title: "Running with Jython"
excerpt: ""
tags:
  - development
  - jython
  - python
  - java
published: true
---

We've started using Jython for a project which requires interoperability with a 3rd-party API. They provide a number of `.java` files (and a tree's-worth of documentation) and that's about it. Since our Java knowledge is somewhat limited we decided it would be best to throw Jython into the mix to get things out quicker and help maintainability.

Since Jython is now at 2.5 we'll probably start using it for more things; the 2.5 release brings decorators into the mix, which _should_ allow us to use it with the thrift libraries. Sure, using straight CPython would be better as Jython doesn't allow installation of Python modules written in C, but sometimes you're stuck having to use a specific Java library because there's no comparable one in Python.

One useful way to get pure-python modules compiled into Jython is by using the `easy_install` tool. Getting `easy_install` to work with Jython is pretty easy. Here's an example of installation and usage:

    ~# wget http://peak.telecommunity.com/dist/ez_setup.py
    ~# jython ez_setup.py
    ~# ln -s $JYTHON_HOME/bin/easy_install \
       /usr/local/bin/jython_easy_install
    ~# jython_easy_install simplejson

There's not much more to it. Just be reminded that this will only work with pure-python modules. For C-based modules you'll be better either looking for a pure-python counterpart or a comparable Java library.
