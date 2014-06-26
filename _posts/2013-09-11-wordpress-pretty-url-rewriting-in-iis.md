---
layout: post
title: "Wordpress Pretty-URL Rewriting in IIS"
excerpt: ""
tags:
  - development
  - iis
  - wordpress
published: true
---

The quickest, and in my opinion the safest[^1], way to get pretty-URLs working in IIS is to create a custom 404 handler. This `wp-404-handler.php` file is here:

    <?php
    $qs = $_SERVER['QUERY_STRING'];
    $pos = strrpos($qs, '://');
    $pos = strpos($qs, '/', $pos + 4);
    $_SERVER['REQUEST_URI'] = substr($qs, $pos);
    $_SERVER['PATH_INFO'] = $_SERVER['REQUEST_URI'];
    include('index.php');

It's a simple thing, but it works pretty well. Just add this file to your wp root directory and point IIS's 404 handler to that file (URL, not File). A free, 2 minute fix to a problem **that shouldn't exist**[^2].

[^1]: My own experience has been that installing any third-party extension for IIS is time-consuming, costly, and breaks IIS in very unexpected ways which --- even after an uninstall --- is a nightmare to fix. YMMV.

[^2]: IIS should've had rewrites bundled as-of IIS4. AFAIK they're still not available even in IIS7!
