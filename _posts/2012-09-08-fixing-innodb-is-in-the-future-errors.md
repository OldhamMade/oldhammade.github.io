---
layout: post
title: "Fixing \"InnoDB is in the future!\" errors"
excerpt: ""
category: blog
tags:
  - development
  - mysql
published: true
---

Often, when the MySQL server crashes, the InnoDB log and tables loose their synchronisation and start issuing lines similar to the following to the error log:

    090216  7:01:04  InnoDB: Error: page 51 log sequence number 1209237857
    InnoDB: is in the future! Current system log sequence number 1209236508.
    InnoDB: Your database may be corrupt or you may have copied the InnoDB
    InnoDB: tablespace but not the InnoDB log files. See
    InnoDB: http://dev.mysql.com/doc/refman/5.1/en/forcing-recovery.html
    InnoDB: for more information.

I've found the quickest way to fix this is to use mysqldump to get a snapshot of your DB, drop the DB, and recreate it using the dump. As a manual process (using tools such as phpMyAdmin or Navicat) this can be quite slow, but from the unix commandline you can issue the instructions in a couple of lines:

    # mysql -e "CREATE DATABASE tmp_db;" && mysqldump -Ccq old_db | mysql tmp_db
    # mysql -e "DROP DATABASE old_db;"
    # mysql -e "CREATE DATABASE new_db;" && mysqldump -Ccq tmp_db | mysql new_db

You'll need to remember to include other options, but the main guts are there.
