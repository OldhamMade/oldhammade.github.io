---
layout: post
title: "Useful buildout recipes"
excerpt: ""
category: blog
tags:
  - development
  - buildout
  - python
published: true
---
`zc.buildout` is a great way to manage project dependencies. It's much more useful than `virtualenv`
because of the number of recipes that are available, and the fact that you can roll your own
if you can't find the functionality you desire. It makes deployment across machines easy
and when you're working in a large or distributed team it helps enforce development strategies
that ensure everyone is up-to-date and working in the right way.

Over the years I've come across some really handy recipes, which I'll outline below.

***

## mkdir

The recipe `z3c.recipe.mkdir` can generate directories within a buildout. It's really handy for
creating `tmp`/`log` directories ready for your program to use.

Not only that, it can help guard against common errors associated with missing directories for
production deployments. I've seen a number of cases where deploying to a new machine which doesn't
have, for example, an `uploads` directory can cause issues when trying to upload files. `mkdir`
can help guard against that, especially if your tests also require these directories to exist.


## sphinx

If you use Sphinx for generating documentation `collective.recipe.sphinxbuilder` is worth looking at.
Having an easy way for your developers to build and review documentation extracted from docstrings
helps promote documentation as a "first-class citizen".


## lxml

If you use `lxml` in your project I'd suggest looking at `z3c.recipe.staticlxml` -- it will build a
*static* version of the lxml egg; that is, it won't have any dependencies on libxml2 and libxslt.
This can get around a host of headaches that installing `lxml` can cause, and should make your
project more easy to work with across platforms (eg. Linux and OS X).
