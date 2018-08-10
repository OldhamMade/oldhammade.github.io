---
layout: post
title: "Querying for Entities with Ancestors with a partial Key"
excerpt: "Retrieve an Entity which has Parents when you only have the Entity's Key"
category: development
tags:
  - Google Datastore
  - GQL
---

I've been doing some work with [Google Datastore](https://cloud.google.com/datastore/) recently. It's a great NoSQL platform, though it doesn't yet have the following of offerings such as Amazon's DynamoDB, and therefore suffers from a lack of useful articles explaining approaches to common, if not mainstream, techniques.

One tricky technique I recently had to navigate was to retrieve an Entity which has Parents when you only have the Entity's Key. Below is an example of the approach I took.

***

Let's say we have an Entity with a kind of `Class`, and a number of `Student` Entities which belong to that `Class`:

    Class: Maths, KEY('Class', 'C1')
     ├─ Student: Amy, KEY('Student', 'S101', 'Class', 'C1')
     └─ Student: Andy, KEY('Student', 'S102', 'Class', 'C1')

Now let's say that in the school's enrollment system an Administrator wants to see information about the Student. So, the Administrator follows a URL in the form of `/students/S101`.

If you know the entire key, or both the parent and child keys, it's relatively easy to retrieve the `Student` Entity:

    SELECT * FROM Students WHERE __key__ = KEY('Student', 'S101', 'Class', 'C1')

However, this doesn't seem to work if you only know the child part of the key, for instance `S101` in our example.

I found very little about this in the [online documentation](https://cloud.google.com/datastore/docs/concepts/overview). Some vague references here and there, but nothing concrete.

Initially I hoped something like the following might be available:

    SELECT * FROM Students WHERE __key__.name = 'S101'

But unfortunately this isn't the case.

What *does* work, however, is to use the keyword `CONTAINS` with a "partial" key:

    SELECT * FROM Students WHERE __key__ CONTAINS KEY('Student', 'S101')

This should also work for nested hierarchies where you only have parts of the path:

    SELECT * FROM Students WHERE __key__ CONTAINS KEY('Class', 'C1') AND __key__ CONTAINS KEY('Building', 'B4')

***

I have yet to do performance checks to see how this compares with lookups using the full key. Google Datastore, while useful due to it's flexibility, isn't really geared towards performance anyway, so local caching of query results is usually recommended, which in this case would mitigate performance issues.
