---
layout: post
title: How to fix a hanging docker command on macOS
excerpt: "If executing `docker` is slow, this might be the cause."
category: tip
tags:
  - macOS
  - docker
  - docker-machine
---
It's been a little while since I've used `docker`, and I found that running the command on
the terminal would simply hang, even when running `docker -v`. A quick check showed that it
would take around 32s to run:

  $ time docker -v
  Docker version 17.06.0-ce, build 02c1d87
  docker -v  0.01s user 0.02s system 0% cpu 32.064 total

After some digging around, I found that this was because I had some old `DOCKER_*` env vars
knocking about. You can check this by running the following:

  $ set|grep DOCKER
  
The super simple fix was to make sure my docker machine was running, and then eval 
the `docker-machine env` command, thusly:

  $ eval $(docker-machine env my-machine)
  
It seems that the `docker` command was simply timing out when trying to connect to the machine;
spinning up a machine to respond, and setting the correct env vars, and the problem goes away.
