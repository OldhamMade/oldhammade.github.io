---
layout: post
title: "Stop using usernames!"
excerpt: ""
category: article
tags:
  - development
published: true
---
This is getting rather irksome now. As a developer, it's easy to see how other people's work can be
made so much better with a negligible tweak here and there, something that wouldn't take the owner/dev
long to implement but would be really beneficial to the end-user.

The one I come across most often? Usernames.

When I'm registering for a site/service, I hit this box and always pause. I don't actually want to
fill it out. I really don't. It's forcing me to create a persona by which I will always be known on
that system. If I don't use that system much, I'm bound to forget the username. And this is where things
start to get tricky, as with a lot of systems (I'm looking at you, PHPBB) *you can't recover your account
without knowing your username*.

Often times systems require usernames to be unique. This is **horrible** when you're trying to register
and you find that your usual username has been taken (stolen!!!) by another individual. Then you have to
spend another 10 minutes trying to find an alternative or modification you're happy with, or you give in
and use `myusualname_1292` and then instantly forget it. Then you come to log in a few weeks later and...
nope. Stuck. Can't get back in.

One solution would be to provide authentication via OpenID. It's simple for the user, for the most part,
as they probably already have an OpenID account somewhere. And if they don't, there are a whole host of
providers out there who can take away the hassle of managing account details for you and your platform.
Except that they don't, as you still need to link the OpenID accounts with information/activity in your
system, then there's preferences your user may need to manage... and it continues to get complicated.

There's actually a really simple solution to this. Just replace `username` with `email`. Done.

There are a number of benefits to using email addresses:

- Users are pretty good at remembering their email address. Sure, they may have
more than one, but it's almost guaranteed that they have fewer email addresses to remember than usernames
they've accumulated over the years.
- They're unique by default.
- If the user forgets their password, they don't need to remember an obscure username to retrieve it.

If you need to display a unique identifier for the user, just ask the user for a "Display name" *after*
they've registered.

Why this isn't common practice eludes me.
