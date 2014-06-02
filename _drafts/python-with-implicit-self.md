---
layout: post
title: "Python: with implicit self"
excerpt: ""
category: blog
tags:
  - development
  - python
published: true
---
I love Python. Having worked with it for nearly 10 years, I'd consider it my primary language now. I love it's rules, it's requirements, it's structure. But as with everything, there are some annoyances...

One thing that we often do as Python developers is create a number of object attributes in the `__init__` method on classes. This can end up looking like a wall of text though:

    import os
    class Foo(object):
        def __init__(self, spam, eggs, parrots, knights, debug=False):
            self.spam = os.path.abspath(spam)
            self.spamdir = os.path.basedir(self.spam)
            self.eggs = os.path.join(self.spamdir, eggs)
            self.debug = debug
            ...

Yes, there are probably nicer ways to do things like the above, but there are those occasions when your `__init__` method accepts a number of arguments, does some small manipulations to them, and hooks them onto `self` for use by your other methods.

It's a little niggle, but I'd love to see this rule: when the `with` statement is used within a class method and is passed the `self` or `cls` instance, all assignments within that block are assigned to the instance/class.

This would really help tidy-up these blocks:

    import os
    class Foo(object):
        def __init__(self, spam, eggs, parrots, knights, marmalade):
            with self:
                spam = os.path.abspath(spam)
                spamdir = os.path.basedir(self.spam)
                eggs = os.path.join(self.spamdir, eggs)
                ...

I know, it's not much. It really is a little niggle, but you do feel you can afford to have these niggles when you live with Python; there's not much else to be annoyed about!
