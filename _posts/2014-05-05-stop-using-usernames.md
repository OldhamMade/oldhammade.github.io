---
layout: post
title: "Stop using usernames!"
excerpt: "Seriously. It will make things much easier for your users."
category: article
tags:
  - development
  - usability
published: true
---
As a developer, it’s easy to see how other people’s work could be made so much better with a minimal tweak here and there. Something that wouldn’t take the owner/dev long to apply yet would be beneficial to the end-user.

The one I come across most often? Usernames.

When I’m registering for a site/service, I hit this box and always pause. I don’t actually want to fill it out. I really don’t. It’s forcing me to create a persona by which I will henceforth be known on that system. Often this username can't be changed, so whatever I choose, I'm stuck with.

If I don’t use that system much, I’m bound to forget the username. This actually happened recently when I registered for EuroPython 2014. I registered early --- it will be my first EuroPython, so I was quite keen! --- and then didn’t access the site again until I got a reminder email asking me to make sure my details were up to date. I opened the site to do so and... um... what was my username again?

And at this point things can start to get tricky, because with a lot of systems --- I’m specifically looking at *you*, PHPBB --- **you can’t recover your account without knowing your username**. [^1]

Often, systems dictate that usernames are to be unique. It's horrible when you’re trying to register and you find that your usual username has been taken by another individual -- some may even consider their username to have been stolen! Then you have to spend another 10 minutes trying to find an alternative or modification you’re happy with. Or you give in and use `myusualname_1292` which you promptly forget it as soon as you click "submit". Then you come to log in a few weeks later and… nope. Stuck. Can’t get back in.

One solution that is becoming popular is to provide authentication via Google/Facebook/Twitter/OpenID. It’s simple for the user, for the most part, as they probably already have an account they can use. And if they don’t, they can quite easily get one.

From the developer's perspective, it's great too --- it takes away the hassle of managing account details within your platform. Except, that's not quite true, as you still need to link the external account with the user's information and activity in your system. Then there’s preferences your user may need to manage, both within your system and with the external provider...

Don't get me wrong --- I'm a fan of these solutions. Usually. But like many other people, I don't always want to tie one of my accounts with a site I'm trying to register with. Maybe after using it for a few weeks, I'll take the final step and link things up. For now, just let me sign up quickly.

However, there is a very simple and elegant solution to all these headaches:

**Just replace `username` with `email`.**

Done.

There are a host of benefits to using email addresses:

- Users are pretty good at remembering their email address. Sure, they may have more than one, but it’s almost guaranteed that they have fewer email addresses to remember than usernames they’ve accumulated over the years.
- People can get quite attached to their online personas, so to find that someone has used your usual username can be irksome. This cannot happen with emails.
- They’re unique by default.
- If the user forgets their password, they don’t need to remember an obscure username to retrieve it.

Management of accounts within your system becomes much easier. And if you need to display a unique identifier for the user, just ask the user for a “Display name” after they’ve registered. Most people would prefer to be referred to by their first name than their username, anyway.

Why this isn’t standard practice eludes me.

[^1]: Thankfully, the EuroPython support team responded to my username-enquiry email within minutes. But I've not been so lucky with other sites/systems.
