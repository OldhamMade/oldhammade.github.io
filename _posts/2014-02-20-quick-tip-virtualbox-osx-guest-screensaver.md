---
layout: post
title: Quick tip &#8212; Don't set a screensaver on OS X Virtualbox guests
excerpt: ""
tags:
  - OS X
  - Virtualbox
---
On occasion I use a Virtualbox OS X guest instance on my OS X host for certain types of work. Things like connecting to a VPN, running test builds, or any time I need to do something that could mess up my local environment in a way I wouldn't be able to fix quickly or easily.

One thing I noticed recently was that occasionally the fans would kick-in on my Macbook Air while I had this guest running. My fans rarely kick in, so I decided to investigate.

I found that my guest had been idle long enough for the screensaver to kick-in. The screensaver was set to "Flurry" with the default parameters. It seems that this was taxing for the VM to render, thus causing my MBA's CPU to get hot and the fans to activate.

Disabling the screensaver and setting the display to turn off after 2 mins fixed the problem.
