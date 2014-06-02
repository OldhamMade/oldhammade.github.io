---
layout: post
title: "Setting the screen resolution for an OS X guest on Virtualbox"
excerpt: ""
category: article
tags:
    - OS X
    - Virtualbox
published: false
---

    vboxmanage setextradata "VM name" VBoxInternal2/EfiGopMode N

Where N can be one of 0,1,2,3,4 referring to the 640x480, 800x600, 1024x768, 1280x1024, 1440x900 screen resolution respectively.
