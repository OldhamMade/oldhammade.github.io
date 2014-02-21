---
layout: post
title: "From PHP to Python; x for y."
excerpt: "Recently I've been using Python more and more for "
tags: 
- development
- php
- python
published: true
---

Recently I've been using Python more and more for programming tasks, but there are still some areas where I find myself thinking "how the heck to I do _x_ in Python? In PHP its just one little function!" This probably stems from the fact that I learned programming from the PHP manual, and one of the reasons PHP has become so prevalent in the programming world is that it has lots of little "short-cut" functions which just do that something you've been looking for in one concise bit of code.

### file_get_contents() in Python

This one always gets me. Python has no exact swap-in method for this. Sure, if you were to do it the correct way in PHP you'd open a file handle, read from it until there was nothing left to read, and close it. Its the same in Python. The problem is that once you learn about file_get_contents() in PHP you start to rely on it for most file operations -- which, when you think about it, are generally "get everything in this file and put it into this variable."

The simplest way of doing this in Python is:

    f = file('/path/to/file').read()

You can also mimic the PHP file() function with:

    f = file('/path/to/file').readlines()

And to mimic file_put_contents():

    file('/path/to/file', 'w').write(contents)

Keep in mind, however, that this solution doesn't have stream support built-in like PHP has. I'm hoping there is something as ubiquitous as PHP's stream support in Python3.0, but a quick flick through the docs hasn't brought anything up.

### parse_ini_file() in Python

Again, no exact swap-in method, but this time I'm not too fussed; Python has a more powerful module called [ConfigParser](http://docs.python.org/library/configparser.html). Don't bother rolling your own, just use this. It works, its better, and you can extend it however you want.

### SimpleXML in Python

Python has a plethora of modules for working with XML. SimpleXML is designed to be the simplest and fastest interface for working with XML in PHP. For Python it seems the fastest and simplest module for working with XML is cElementTree, which is bundled by default with Python2.5 and later.

When you're looking for a more complete system akin to DomDocument then lxml seems a good fit.

Now, before those of you knowledgeable in Python-Fu start throwing kicks, keep in mind: I'm not _that_ familiar with Python yet. I don't yet know its idiosyncrasies, foibles, best-practices, and tricks. If I'm missing something then please, __please__ let me know. I love Python's concise syntax, and if I can trim even more lines from my code I'll be happy to take your suggestions!
