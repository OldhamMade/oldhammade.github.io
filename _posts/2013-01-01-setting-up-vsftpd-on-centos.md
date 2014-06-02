---
layout: post
title: "Setting up vsftpd on CentOS"
excerpt: "I've always found setting up vsftpd a bit of a pain, so here are some simple instructions to follow and help with a few \"gotchas\"."
category: article
tags:
  - server
  - devops
published: true
---

"vsftpd" stands for "Very Secure File Transfer Protocol Daemon", and is one of the easier FTP daemons to install. Despite this, I've always had to battle with it to get it configured correctly, but I always find it's usually down to configuring it in a rush or in the "background" while doing other things.

Notes
-----

The commands below are being run a priviledged user. Remember to prefix `sudo` if you're running the commands as an unpriviledged user.

Also, I use `mg` as my main text editor, which is an [simple emacs clone](http://en.wikipedia.org/wiki/Mg_(editor)). Feel free to use `nano`, `vi`, or any other program in it's place.

Installation
------------

If it's not already installed, nstalling vsftpd on CentOS is as simple as:

    $ yum install vsftpd

You'll probably want to set up vsftp so it starts up with all the other services on boot:

    $ chkconfig add vsftpd
    $ chkconfig vsftp on

Configuration
-------------

Firstly we'll set up an FTP group:

    $ groupadd ftpusers

...and an FTP-specific user:

    $ useradd -G ftpusers -d /path/to/your/dir -s /sbin/nologin ftpuser

The `/sbin/nologin` shell should be listed in `/etc/shells` by default on CentOS. If not, find the location of your `nologin` binary and add the path to the end of the file.

Then we'll add a password for the user:

    $ passwd ftpuser

Next we need to make sure that this new user has permission to read and write the directory:

    $ chown -R ftpuser /path/to/your/dir
    $ chmod 775 path/to/your/dir

Now we can configure the daemon itself. Firstly, stop the daemon if it's already running:

    $ service vsftpd stop

Then we can edit the main config file:

    $ mg /etc/vsftpd/vsftpd.conf

...making the following changes:

Disable anonymous login:

    anonymous_enable=NO

Enable local users:

    local_enable=YES

The ftpuser should be able to write data:

    write_enable=YES

Port 20 need to turned off, makes vsftpd run less privileged:

    connect_from_port_20=NO

Chroot everyone:

    chroot_local_user=YES

Umask should be already set to 022 in the default config file, which makes sure that all the files and folders that are uploaded receive the proper permissions (644 and 755, respectively).

    local_umask=022

We also need to add the following lines to add the FTP user we created earlier:

    # the list of users to give access
    userlist_file=/etc/vsftpd/vsftpd.userlist
    # this list is on
    userlist_enable=YES
    # It is not a list of users to deny ftp access
    userlist_deny=NO

Then save those changes and exit.

Next we need to create the userlist file we've just assigned:

    $ /etc/vsftpd/vsftpd.userlist

...and add the user:

    ftpuser

Save these changes and exit.

We should be good to go, so let's start the vsftpd:

    $ service vsftpd start

If we've been successful, we should be able to access the ftp server. Fire up another terminal instance and try it:

    $ ftp ftpuser@yourhost
    Connected to yourhost.
    220 (vsFTPd 2.2.2)
    331 Please specify the password.
    Password:

Enter your password and you should be in!

Gotchas
-------

If you're having trouble here are a few things to check:

Firstly, check all the paths you've entered. I know it seems silly, but this is usually the cause. Checking the path for the `nologin` shell, for the userlist, etc.

SELinux always seems to get in the way. A lot of posts will tell you to simply disable it. This advice should be considered harmful. Instead, you can simply enable FTP access in SELinux using the following commands.

    $ setsebool -P allow_ftpd_full_access 1
    $ setsebool -P ftp_home_dir=1

Further information on SELinux boolean flags can be found on the [CentOS website](http://wiki.centos.org/TipsAndTricks/SelinuxBooleans).
