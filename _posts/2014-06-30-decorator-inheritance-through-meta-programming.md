---
layout: post
title: "Decorator inheritance through meta-programming"
excerpt: "Complex is better than complicated. At least for this project."
category: blog
tags:
  - development
  - python
  - meta-programming
  - decorators
published: true
---

### Scenario ###

I recently completed a really fun project for a client in which I designed and built a framework which would orchestrate interaction between discrete components. Each component did [OneThingWell&#153;](http://en.wikipedia.org/wiki/Unix_philosophy#Doug_McIlroy_on_Unix_programming) and could be composed into different workflows based on the data that was being processed.

I had a hand in building the first few components but then that task was to be taken on by both on-shore and off-shore teams, and most of these developers were new to Python. Because of this, I needed to set up some simple conventions that could be followed, and to make everything as simple as possible for the new devs who were coming on board and creating these components.

While each component was discrete, there was cross-cutting functionality that affected all components which had to be taken into consideration, such as logging and error management. Trying to keep the components simple, while still implementing the cross-cutting functionality, was going to be somewhat of a challenge.

### Solution

I specifically didn't want to have the devs pepper their code with things they didn't really understand. In fact, because some of the devs were learning Python specifically for this project, I felt that they should only need to create a simple class-callable that inherited from a base-class and then fill out the `__init__` and `__call__` methods. That's it.

And that's what they got, through meta-programming.

The first step was to create the class from which we'll inherit our main functionality:

    class BaseComponent(object):
        """
        Base class for components.
        """
        def __call__(self, *args, **kwargs):
            raise NotImplemented('The __call__ method must be overridden')

        # ... a number of inherited methods ...

In here we might add utility methods for database access, stuff like that.

Next, I created a meta-class which applies the decorators:

    from .decorators import *

    class MetaBaseComponent(type):
        """
        MetaClass used to enforce decoration of the __call__ method of
        classes that inherit from the BaseComponent class
        """
        def __new__(cls, name, bases, clsdict):
            decorator_chain = (LogExecution, LogErrors,)

            if '__call__' in clsdict:
                for decorate in reversed(decorator_chain):
                    clsdict['__call__'] = decorate(clsdict['__call__'])

            return super(MetaBaseComponent, cls).__new__(cls, name, bases, clsdict)

Here I'm creating a new *type*, and by changing the way `__new__` is executed I'm jumping in before `__init__` is called on the child classes. Our decorators are applied at this point around the `__call__` method, if it exists.

***

### Aside:
I'm using a loop to apply the decorators from a tuple so I can easily add more decorators at a later date, but in this example lines 9:13 could be simplified to the following:

            if '__call__' in clsdict:
                clsdict['__call__'] = LogErrors(LogExecution(clsdict['__call__']))

***

Then I need to add this new type (meta-class) to the base class by setting it as the `__metaclass__` (line 5):

    class BaseComponent(object):
        """
        Base class for components.
        """
        __metaclass__ = MetaBaseComponent

        def __call__(self, *args, **kwargs):
            ...

Now I can simply inherit the base class:

    class ConcreteComponents(BaseComponent):
        """
        Our specific implementation
        """
        def __call__(self, ...):
            # do stuff here...


...and when `__call__` is executed it does so with all the decorated goodness we've previously added.

Sure, some complexity and "magic" is being added, which some would say goes against items 2 & 3 of ["the Zen"](http://legacy.python.org/dev/peps/pep-0020/#content), but I think this lives whole-heartedly in item 4:

> Complex is better than complicated.

And that's just what the devs needed on this project.
