---
layout: post
title: "Fixing timezones in PHP"
excerpt: "Had a little problem recently with PHP on one of o"
tags: 
- development
- php-linux
published: true
---

Had a little problem recently with PHP on one of our servers. I threw the following script onto the server to see what was going on:

    <?php echo date('Y-m-d H:i:s'), "\n", `date`;

It was registering the time an hour out, even though the server was set to the correct date/time (which I wrote about recently).

Delving deeper, I checked the php.ini file was set to "GMT" which is an exact timezone. It was early, and the ol' brain wasn't running at full capacity, so I hit Google and came across [this article](http://www.electrictoolbox.com/correct-php-timezone/) which explains a very long-winded solution to the problem. Even with it being early the solution didn't sit well with me. 

Then I remembered: the correct way to set the timezone is to use the location of the server. So, I set it to "Europe/London", restarted the PHP processes (we're using FastCGI), and all was well.
