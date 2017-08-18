---
layout: post
title: "Querying for Entities with Ancestors with a partial Key"
excerpt: "If executing `docker` is slow, this might be the cause."
category: development
tags:
  - Google Datastore
  - GQL
---
Let's say we have an Entity with a kind of `Class`, and a number of `Student` Entities which belong to that `Class`:

    Class: Maths, KEY('Class', 'C1')
     `Student: Amy, KEY('Student', 'S101', 'Class', 'C1')
     `Student: Andy, KEY('Student', 'S102', 'Class', 'C1')

Now let's say that in the school's enrollment system an admin wants to see information about the student. So, the admin follows a URL in the form `/students/S101`.

If you know the entire key, or both the parent and child keys, it's relatively easy to retrieve the `Student` Entity:

    SELECT * FROM Students WHERE __key__ = KEY('Student', 'S101', 'Class', 'C1')

However, this doesn't seem to work if you only know the child part of the key, for instance `S101` in our example.

I found very little documentation online. Some vague references here and there, but nothing concrete.

I hoped something like the following might be available:

    SELECT * FROM Students WHERE __key__.name = 'S101'

But unfortunately this doesn't work.

What *does* work, however, is to use the keyword `CONTAINS` with a "partial" key:

    SELECT * FROM Students WHERE __key__ CONTAINS KEY('Student', 'S101')

This should also work for nested hierarchies where you only have parts of the path:

    SELECT * FROM Students WHERE __key__ CONTAINS KEY('Class', 'C1') AND __key__ CONTAINS KEY('Building', 'B4')
