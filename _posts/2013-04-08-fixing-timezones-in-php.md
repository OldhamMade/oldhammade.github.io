---
layout: post
title: "Fixing timezones in PHP"
excerpt: "Quick fix for a server that showed PHP to be an hour \"out\""
tags:
  - development
  - php-linux
published: true
---

Had a little problem recently with PHP on one of our servers. I threw the following script onto the server to see what was going on:

    <?php echo date('Y-m-d H:i:s'), "\n", `date`;

If you've not seen the backticks before, this is just a quick way to execute the contents of the backticks as a shell command. The output will be returned so it can be assigned to a variable, or echo'd.

The script showed that PHP was an hour out, even though the server was set to the correct date/time (which I wrote about recently).

Delving deeper, I checked the php.ini file. The timezone was set to `GMT`, which is an exact timezone. The correct way to set the timezone is to use the location of the server.

Once I set it to `Europe/London`, restarted the PHP processes (we're using FastCGI), all was well.
