---
layout: post
title: Changing OS X system date from Terminal
excerpt: ""
category: blog
tags:
  - OS X
  - command line
---

If you're trying to install OS X Maverics onto an older machine, you may find that you get the
following error message:

> This copy of the Install OS X Mavericks application can't be verified.
> It may have been corrupted or tampered with during downloading.

This may be because the system clock is out of date. You can check this by going to `utilities`
and opening `terminal`, then issuing the following command:

    date

This will give you the current system date, probably set to somewhere around the year 2000. If
this is the case, you can easily change the date using the same `date` command. The format is:

    date {month}{day}{hour}{minute}{year}

So, for example, you could enter:

    date 0101000014

Which will set the date to Jan 1st, 2014.

Update your system to the current date and time, and you should be able to successfully retry
your installation... unless Mavericks *was* actuallyl corrupted during the download!
