---
layout: post
title: "Nginx, Subversion, and 413's"
excerpt: ""
tags:
  - development
  - nginx
  - svn
published: true
---

I spent some time recently migrating a subversion repository off-site. I also took the opportunity to tidy up some of the setup, install [trac](http://trac.edgewall.org/) and create some repositories for unversioned projects.

While pushing one of these unversioned projects, I started seeing `"413 - Request entity too large"` errors which would then kill the commit at that point. The setup was the same as any other nginx+svn install; nginx proxies to apache+mod_svn. I checked the SVN docs without success, however some time spent on google revealed that this was an error with the "LimitRequestBody" option in apache.

The problem was, I hadn't set that option. It wasn't anywhere in the config files. Thinking there might be a very low default value I set it manually to 2Gb and tried again.

**413.**

A few days later I was setting up a new CentOS server with nginx, php, mysql, et al. Since there was a new version of nginx released I spent a few moments reviewing the wiki to see what the changes were, and that's when I came across the `client_max_body_size` directive. From the docs:

> Directive assigns the maximum accepted body size of client request, indicated by the line "Content-Length" in the header of request.
>
> If size is greater the given one, then the client gets the error "Request Entity Too Large" (413).
>
> It is necessary to keep in mind that the browsers do not know how to correctly show this error.

It hadn't occurred to me that nginx would be the issue. The default is a measly 1Mb. Fine if you're being sent simple http requests, rubbish for large uploads like the kind the svn client sends.

Setting `client_max_body_size 1024m;` in the vhost fixed it.
