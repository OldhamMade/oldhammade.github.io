---
layout: post
title: "Why I hate TDD"
excerpt: ""
tags:
  - development
  - python
  - test-driven-development
---

I know, another article with an inflamatory title. But I do. I really do hate Test Driven Development.

But let me clarify that statement. I hate TDD *in Python*. I like testing. I think tests are great. I thin testing in Python is great too. But the way I see TDD tests in Python make me want to claw my eyes out. They're so... unreadable.

One of the primary reasons people use Python is it's readability. There are [rules regarding formatting], there are guidelines on [how to document] our code, there's even [the Zen]. But there's nothing on how to write good tests, specifically test names, in Python.

Some code I worked on recently had a test class that was basically the following:

    class TestProduct(unittest.TestCase):
        def test_description(self):
            ...

I spent some time trying to work out what `test_description` did, and it seemed pretty straight-forward, but for the life of me I couldn't work out *why* the developer hadn't specified *what* they were testing, and what the expected outcome was.

Well, sure, they had described what they were testing. They were testing something to do with the `description` on a `Product`. But at a cursory glance I couldn't work out what they were trying to test. Or, rather, what they were trying to ensure was happening within the test from it's name.

People lament Behaviour-Driven Development practices. They say it's over-complicated and unnecessary. I think they're right. The BDD tools have gotten way to big, they're too much of a time investment.

It doesn't have to be this way. You don't need the stories. You don't need the **Given**, **When**, **Then** scenarios.

It can be really simple. In fact, you only need to do one thing:

**Make the test name describe what you're trying to achieve.**

You already make your variable names descriptive. You make your function/method names descriptive. You write your code so that it tells a little store. Then you give you and write crappy test names. Why?!

Let's make the above example better by adding a little narative element, so you can see what I mean.

    class BasicProductTests(unittest.TestCase):
        """Ensuring that basic interaction with
        Product objects is simple and correct"""

        def test_description_accepts_strings(self):
            ...

        def test_description_raises_when_not_given_strings(self):
            ...

        def test_description_raises_when_empty_on_save(self):
            ...

This will still work with nose. Your tests will still run. And your co-workers won't [stab you in the neck with a pencil].

[rules regarding formatting]: http://legacy.python.org/dev/peps/pep-0008/
[how to document]: http://legacy.python.org/dev/peps/pep-0257/
[the Zen]: http://legacy.python.org/dev/peps/pep-0020/
[stab you in the neck with a pencil]: http://blog.codinghorror.com/coding-for-violent-psychopaths/
