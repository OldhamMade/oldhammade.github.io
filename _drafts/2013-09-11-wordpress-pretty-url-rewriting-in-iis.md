---
layout: post
title: "Wordpress Pretty-URL Rewriting in IIS"
excerpt: "The quickest, and in my opinion the safest, way to"
tags: 
- development
- iis
published: true
---

<p>The quickest, and in my opinion the safest<sup><a href="#footnote-1" style="text-decoration: none; font-weight: bold;">&#8224;</a></sup>, way to get pretty-URLs working in IIS is to create a custom 404 handler. This "<code>wp-404-handler.php</code>" file is here:</p> 

<p><pre>
&lt;?php
$qs = $_SERVER['QUERY_STRING'];
$pos = strrpos($qs, '://');
$pos = strpos($qs, '/', $pos + 4);
$_SERVER['REQUEST_URI'] = substr($qs, $pos);
$_SERVER['PATH_INFO'] = $_SERVER['REQUEST_URI'];
include('index.php');
</pre></p>

<p>It's a simple thing, but it works very, very well. Just add this file to your wp root directory and point IIS's 404 handler to that file (URL, not File). A free, 2 minute fix to a problem <strong>that shouldn't exist<sup><a href="#footnote-2" style="text-decoration: none; font-weight: bold;">&#8225;</a></sup></strong>.</p>

<p style="font-size: .7em;" id="footnote-1"><strong>&#8224;</strong> &#8213; My own experience has been that installing any third-party extension for IIS is time-consuming, costly, and breaks IIS immediately and in very unexpected ways which &#8212; even after an uninstall &#8212; is a nightmare to fix. YMMV.</p>

<p style="font-size: .7em;" id="footnote-2"><strong>&#8225;</strong> &#8213; IIS should've had rewrites bundled as-of IIS4. AFAIK they're still not available even in IIS7!</p>
