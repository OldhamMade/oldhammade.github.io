---
layout: post
title: "Installing Supervisord on OS X Mavericks"
excerpt: ""
category: blog
tags:
  - development
  - python
  - supervisord
published: true
---
Over the years I've found Supervisord to be invaluable for development. It's a
great way to ensure long-running daemons start up and stay up.

I also have it running on my MacBook Air so I can manage services I use for
development without having them running all the time, things like nginx, mysql,
redis, memcached, etc.

Here's how to install it.

## pyenv ##

I'm going to assume you're using `pyenv`, and if you're not you should be -- it
really is the best way to manage multiple Python installs on your local machine.

Since supervisord will be installed globally on the system, I'd recommend that
you use your system's default install of Python. To achieve this, you'll need to
open a new terminal window and switch that terminal instance back to your
system's default Python version, like this:

    > pyenv local system

And check you're running the local version by issuing the following commands:

    > python -V
    > which python

Once you're satisfied you have the right version of Python activated you can now
install supervisord.

## supervisord ##

You can use `pip` or `easy_install`, whatever is convenient for you, but do make
sure that it's the **system** version of Python that's running.

    > easy_install supervisor

Once that's installed, double check that the path to `supervisord` is
`/usr/local/bin/supervisord`. If it is, we can move on and install the plist
file.

## supervisord.conf ##

Now you'll need to create a `supervisord.conf` file:

    > /usr/local/bin/echo_supervisord_conf > /usr/local/etc/supervisord.conf

Feel free to make any edits you believe to be necessary.

## plist ##

Below is the plist you'll be using. Copy/paste this into a file named
`org.supervisord.plist` and save it somewhere handy.

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>KeepAlive</key>
        <dict>
            <key>SuccessfulExit</key>
            <false/>
        </dict>
        <key>Label</key>
        <string>org.supervisord</string>
        <key>ProgramArguments</key>
        <array>
            <string>/usr/local/bin/supervisord</string>
            <string>-n</string>
            <string>-c</string>
        <string>/usr/local/etc/supervisord.conf</string>
        </array>
        <key>RunAtLoad</key>
        <true/>
        <key>Nice</key>
        <integer>20</integer>
        <key>LowPriorityIO</key>
        <true/>
    </dict>
    </plist>

Now you'll need to copy that file into `/Library/LaunchDaemons`. Once complete,
you can load the file into `launchd`:

    > launchctl load /Library/LaunchDaemons/org.supervisord.plist

## Confirmation ##

After issuing that command supervisord should be running. Issue the following
command to confirm:

    > ps aux | grep supervisor

At this point I would suggest restarting your machine to make sure supervisord starts-up
correctly.

Now you can edit your `supervisord.conf` file and tailor your setup as you see fit!
