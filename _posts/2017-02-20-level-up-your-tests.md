---
layout: post
title: "One simple trick to level-up your tests"
tags: 
- development
- tdd
published: true
---

I'll keep this short, because it really is simple. 

When you're writing your test functions/methods, in whatever language:

**Replace `test` with `ensure`.**

Whether you do this mentally as you're creating the test name, or whether you can tweak your system so that your test methods are prefixed with `ensure`, you'll quickly see the benefit of this approach.

Here's a quick (contrived) example in Python:

    from model import User
    
    def test_user():
        user = User()
        user.save()
        assert user.id

Yes, this is a very spurious example, but it is the essence of the kind of tests one might see in the wild. And it drives me crazy.

Let's follow the rule, and tweak the example:

    from model import User
    
    def ensure_user():
        ...
        
I don't know about you, but I want to finish the sentence that starts with "ensure user..." -- I want to state the expectation, the desired outcome. "ensure user... is assigned an ID when saved" feels like a good description of the test.

Let's update the test:

    from model import User
    
    def test_user_is_assigned_an_ID_when_saved():
        user = User()
        user.save()
        assert user.id

Now we know for sure what this test is actually testing. This will help anyone reading it at a later point in time, whether it's someone doing a code review or your future self, a year down the line, trying to remember what the code was supposed to be doing when things are broken, the CI dashboard has gone red, and the client is screaming down the phone to your manager.

Another benefit here is that it shows where the gaps are. "ensure user is assigned an ID when saved" leads us to consider what should happen if an ID isn't set but `save` operation is successful, or what to do if the `save` operation fails. Should we check that saving 2 different `Users` doesn't assign the same ID to both?

I would heartily recommend that, if possible, you change your system so that it can collect tests prefixed with `ensure` rather than `test`. If you're using Python with either pytest or nose, I have a repository [here](https://github.com/OldhamMade/SimpleBDD) which can help you achieve this.
