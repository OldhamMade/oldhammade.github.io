---
layout: post
title: "Subversion and \"/!svn/vcc/default\" errors"
excerpt: ""
tags:
  - development
  - nginx
  - svn
published: true
---

Once again, I come across an odd subversion error which is questioned on various forums but remains unanswered. And again, I find the fault to be with proxying via nginx.

A member of our team came to me today after battling with svn for a few hours trying to push some new files to the server. He couldn't push because his working copy was out of date, and updates failed with the following error:

    svn: REPORT request failed on '/repo/!svn/vcc/default'
    svn: REPORT of '/repo/!svn/vcc/default': 200 OK (http://our.reposerver.tld)

Only a handful of pages came up when attempted some cunning google-fu. I checked out the repository on the server (which completed), and a number of clients on remote boxes (all fails).

Thinking a little more about the error &#8212; a "200 OK" error _isn't_ an error! &#8212; I thought maybe nginx was misbehaving again, and unblocked the port apache was listening on before attempting a check-out through that.

Success!

The nginx error log, which was empty when checked earlier in the day, now had notices similar to the following:

    open() "/etc/nginx/proxy_temp/0/00/0000000000" failed
    (13: Permission denied) while reading upstream

Nginx hadn't created the /0/00/ directory. A quick `rm -rf /etc/nginx/proxy_temp/*` and nginx restart brought things back into line; nginx started creating the directories normally.
