---
layout: post
title: "Unit testing infinite while-loops"
excerpt: "A useful approach to unit testing around infinite while-loops"
category: blog
tags:
  - python
  - tdd
published: true
---
Something that can trip up developers is how to test functions that fall into an
infinite loop, usually done with `while True`. Often developers will skip testing
of these loops, but with only a small change to the loop they can be easily tested
using Python's mock library.

    class Foo(object):
        def start(self):
            while True:
                do_something()
                
    class Foo(object):
        RUNNING = 1  # sentinel value
        
        def start(self):
            while self.RUNNING:
                do_something()
                
                
This allows us to test using mock:

    sentinel = PropertyMock(side_effect=[1, 0])
    type(ob).RUNNING = sentinel
    
    # rest of test
    

