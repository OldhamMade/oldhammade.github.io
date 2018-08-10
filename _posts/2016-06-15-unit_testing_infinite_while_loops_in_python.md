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
Something that can trip developers up is how to test functions that contain an
infinite loop, usually done with `while True`. For example:

    class Foo(object):
        def start(self):
            while True:
                do_something_useful()
                

Often developers will skip testing these scenarios; in this case, the developer may test the `do_something_useful()` method, and leave it at that. However, there may be additional logic inside or after the loop which takes the result of `do_something_useful()` and does further work. This would then go untested, and as the saying goes: 

> **if it's not tested, it's not working.**

With only a small change to the code, and with the use of Python's `mock` library, the loop can be easily tested. 

The goal is to ensure that the loop runs only a fixed number of times. Therefore we can use a [sentinel value](https://en.wikipedia.org/wiki/Sentinel_value) which we can control from our tests, without having to introduce new logic into our code which evaluates whether the code is being run in a unittest or whether it is in production.

Using the example above, we can tweak the code as follows:

    class Foo(object):
        RUNNING = 1  # sentinel value
        
        def start(self):
            while self.RUNNING:
                do_something_useful()
                
                
Then, in our test, we can mock the value of the `RUNNING` attribute and have it change on each evaluation:

    sentinel = PropertyMock(side_effect=[1, 0])
    type(ob).RUNNING = sentinel
    
    # rest of test
    
In this scenario, the first iteration will check the value of `RUNNING` and see it as `1`, a truthy value, and will iterate as normal. At the start of the second iteration, the property will return `0`, a falsy value, and will break out of the loop.

If you need to iterate a specific number of times, the `[1, 0]` list can simply be replaced with (for example) `range(10, -1, -1)`.

We also get the benefit of being able to give the sentinel value an appropriate name which caries some meaning. `while RUNNING` reads better than `while True` or `while 1`, but might not be contextually appropriate. Maybe we're reading from an external resource... `while CONNECTED` might be more fitting. 

Further, since the new sentinel value can be changed from within the running application, it's possible to make use if it to simplify logic controlling whether the loop should run or not. For example, `CONNECTED` might be a memoized property which runs some initial connectivity checks before returning `True`. The function containing the loop therefore doesn't need to know about the state of the connection itself, just that the connection is active.

Happy coding!
