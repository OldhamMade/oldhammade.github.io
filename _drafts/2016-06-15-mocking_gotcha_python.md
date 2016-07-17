---
layout: post
title: "Mocking gotcha in Python"
excerpt: "A useful approach to unit testing around infinite while-loops"
category: blog
tags:
  - python
  - tdd
published: true
---
If you wrap a Mock() in something that uses `__getattr__`, you're gonna have a bad time.
