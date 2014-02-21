---
layout: post
title: "Thrift & Python 2.6: troubleshooting installs"
excerpt: ""
tags:
  - development
  - python
  - thrift
published: true
---

Had a little trouble trying to install [Thrift](http://incubator.apache.org/thrift/) on CentOS5 with Python 2.6. Setting the `PY_PREFIX` environment variable doesn't work; the compile process just ignores it and picks the first python it can find -- usually 2.4.

Quickest way I've found to get things back on track is to rename the /usr/bin/python binary to python2.4, symlink the python2.6 binary in its place, and proceed with the thrift build. Once done, replace the symlink to 2.6 with one to 2.4.

It's hacky, but it works.

Hopefully the thrift developers will fix this in coming releases.
