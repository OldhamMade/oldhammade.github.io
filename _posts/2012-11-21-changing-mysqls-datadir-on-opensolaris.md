---
layout: post
title: "Changing MySQL's datadir on OpenSolaris"
excerpt: ""
category: blog
tags:
  - server
  - opensolaris
published: true
---

As we all know, OpenSolaris is great, but if you come from a RedHat/Debian background things can be a little confusing. This is especially true when setting up common software you've done many times before.

If you need to change the datadir for a fresh MySQL install, for instance to take advantage of ZFS volumes, try following the steps below.

Firstly, create the new data dir, and change ownership to the `mysql` user.

    ~# mkdir /mysqldatadir
    ~# chown -Rf mysql:mysql /mysqldatadir

Edited the file `/var/svc/manifest/application/database/mysql_51.xml`, changing the value of the `data` node.

Stop the service then delete and reimport the manifest file using `svccfg`.

    ~# svcadm disable mysql
    ~# svccfg delete mysql
    ~# svccfg import /var/svc/manifest/application/database/mysql_51.xml

Restart the service.

    ~# svcadm enable mysql

Test everything is working as expected.

    ~# mysql -e "show variables" | grep datadir

Hopefully that will get you where you need to be.
