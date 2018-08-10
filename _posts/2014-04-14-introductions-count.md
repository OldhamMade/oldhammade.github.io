---
layout: post
title: "Introductions count"
excerpt: "A strong introduction counts, especially for software."
tags:
  - development
  - usability
published: true
---

I'm always on the hunt for new, useful open-source tools that can save me and my clients time (and money), and there's something I've noticed over the years --- the most successful projects have a great introduction.

It doesn't take much: a short paragraph displayed prominently on the homepage stating clearly what the project is/does and, importantly, how it can benefit me as a user.

It's so simple it often gets overlooked.

For instance, here's a good example from [Django](https://www.djangoproject.com/):

> Django is a high-level Python Web framework that encourages rapid development and clean, pragmatic design.
>
> Developed by a fast-moving online-news operation, Django was designed to handle two challenges: the intensive deadlines of a newsroom and the stringent requirements of the experienced Web developers who wrote it. It lets you build high-performing, elegant Web applications quickly.
>
> Django focuses on automating as much as possible and adhering to the DRY principle.

In contrast, here's [TidyLib](http://tidy.sourceforge.net/)'s intro:

> A quorum of developers have pitched in on a SourceForge project to maintain and further develop Dave Raggett's excellent HTML Tidy program. We have two primary goals. First, to provide a home where all the patches and fixes that folks contribute can be collected and incorporated into the program. Second, a library form of Tidy has been created to make it easier to incorporate Tidy into other software.

If you don't know what `HTML Tidy` is/does, that intro is relatively useless. There's no link to the `HTML Tidy` project, so you'll have to rely on Google to find out what it is. A small reworking of the above would make things much clearer. Maybe something like:

> TidyLib is a library version of Dave Raggett's excellent HTML Tidy program, which fixes and reformats malformed HTML into something more usable. TidyLib is designed to be more easily integrated into other software, and incorporates a number of community contributed patches and fixes.

That's a mild example. Here's a buzz-word heavy introduction to [Eucalyptus](//open.eucalyptus.com/):

> Eucalyptus - Elastic Utility Computing Architecture for Linking Your Programs To Useful Systems - is an open-source software infrastructure for implementing "cloud computing" on clusters. The current interface to Eucalyptus is compatible with Amazon's EC2, S3, and EBS interfaces, but the infrastructure is designed to support multiple client-side interfaces. Eucalyptus is implemented using commonly available Linux tools and basic Web-service technologies making it easy to install and maintain.

I've been using Virtual Machines for over 10 years, and Amazon's platform for over 6, so all that makes sense to me. That's what Eucalyptus *is*. But I still don't know what Eucalyptus *does* and how it might be useful to *me*.

I've seen it so many times with open-source projects; the very clever guys who design and build these libraries obviously have years on me and my peers in terms of skill, and it shows in the descriptions they write for these projects. They're developers --- they're used to writing terse copy to describe what they're doing for other developers to read. There's nothing wrong with that.

Except that they often forget that not everyone who would like to make use of their project is at their level.

Sometimes the words you use when describing a technology are just too ambiguous for the people reading it. The [KISS principle](http://en.wikipedia.org/wiki/KISS_principle) doesn't just apply to source-code.

Thankfully the fix is simple: **Imagine all your visitors are on the first day of a CS course, and that English is their second language.**
