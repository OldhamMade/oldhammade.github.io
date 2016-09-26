---
layout: post
title: Useful Docker shell aliases, functions, and notes
excerpt: ""
category: tip
tags:
  - Docker
  - bash
  - zsh
---
Some useful shell aliases, functions, and notes if you use Docker.

***

Whenever you start a new Docker machine, you'll also need to evaluate some environment
variables so that the `docker` command knows which machine you're interested in. It can
get pretty tedius, so I use the following shell function/alias to save my sanity:

    docker_machine_env() {
        eval $(docker-machine env $1)
    }
     
    alias dme=docker_machine_env

Now I simply `docker-machine start default` and `dme default` to get up and running quickly.

***

If you see a message similar to the following when trying to start your Docker machine:

    VBoxManage: error: The machine 'default' is already locked for a session (or being unlocked)
    
use:

    $ vboxmanage list vms
    
to get a list of your Docker machine VMs, find the corresponding UUID for your the machine (default
in the example above) and issue the following command:

    $ vboxmanage startvm {vm-uuid} --type emergencystop

You may see some errors about `The machine 'default' is not locked by a session` but these can be ignored.
Your machine should start as normal. 

This happens reasonably often for me, since I work on a laptop. To save time, I have the following alias:

    docker_machine_force_kill() {
        vboxmanage startvm $(vboxmanage list vms | grep $1 | awk '{print $2}') --type emergencystop 2>&1
    }
     
    alias dmfk=docker_machine_force_kill

A simple `dmfk default; docker-machine start default` will get me back up and running.
