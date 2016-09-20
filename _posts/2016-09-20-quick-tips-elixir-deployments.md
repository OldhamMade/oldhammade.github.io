---
layout: post
title: Quick tips for Elixir deployments
excerpt: ""
category: tip
tags:
  - Elixir
  - Distillery
  - exrm
---
Just some quick notes around Elixir deployments, in no particular order...

***

In tutorials, where to see `exrm`, be sure to use [Distillery](https://github.com/bitwalker/distillery).

***

If you see an error like the following:

    [info] Application myapp exited: MyApp.start(:normal, []) returned an error: shutdown: failed to start child: MyApp.Endpoint
        ** (EXIT) shutdown: failed to start child: Phoenix.CodeReloader.Server
  
...try rerunning the release with both `MIX_ENV` and `--env` set to the same env. For example:
   
    MIX_ENV=prod mix release --env=prod
