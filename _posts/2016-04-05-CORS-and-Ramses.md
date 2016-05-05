---
layout: post
title: "CORS and Ramses"
excerpt: "Quick hint if you're having CORS trouble with Ramses"
category: blog
tags:
  - python
  - CORS
  - javascript
published: true
---
Recently I used [Ramses](http://ramses.tech) to quickly knock-up a mock service for a React developer 
I'm working with, so he could make headway while the team built-out the API
he would eventually use.

If you've not seen [Ramses](http://ramses.tech) it's a great little framework for knocking up RESTish
APIs quickly.

One issue we found out pretty quickly is that the documentation for CORS in Ramses is non-existant, and
those for [Nefertari](https://github.com/ramses-tech/nefertari), the REST API framework Ramses uses 
on top of Pyramid, [is minimal at best](http://nefertari.readthedocs.io/en/stable/auth.html?highlight=cors).

Following the docs will only get you half-way there. What you'll _also_ need to do is add the `options`
method in your `RAML` config for the root endpoint, so that the CORS preflight check passes.

For example:

    /api:
        get:
            description: ...
        options:
            description: ...
        post:
            description: ...
            
Hope this helps!
