---
layout: post
title: "for...else in Python should be considered harmful"
excerpt: ""
category: article
tags:
  - development
  - python
published: false
---

Big (and potentially career-destroying!) statement:

### The `else` block for a `for` statement in Python should be considered harmful.

Well, to devs new to Python, anyway. As you start out in a new language while having a
background in another, you look for the keywords which make sense to you to get
a "handle" on things. My first thoughts when seeing the `else` keyword
after a `for` was "if there aren't any items to iterate over, execute
the else so you don't get an error message."

Nope, that's incorrect.

From the docs:

> Loop statements may have an `else` clause; it is executed when the loop terminates
> through exhaustion of the list (with `for`) or when the condition becomes false
> (with `while`), but not when the loop is terminated by a `break` statement.

Which does make some sense, especially when you look at the syntax around `try`/`except`.
However, in my opinion it would make _much_ more sense for a `then` keyword in this instance. 
For example:


    for x in my_list:
        print x
    then:
        print "success!"
    else:
        print "the list was empty!"

This makes a bit more sense to a new user, and cleans up the language as you don't need to test whether a
list is empty, just provide a case for it in the `else`.
