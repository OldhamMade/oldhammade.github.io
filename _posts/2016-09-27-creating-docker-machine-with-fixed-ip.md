---
layout: post
title: Creating a Docker Machine with a fixed IP
excerpt: "If you run multiple docker machines, pinning their IP can be a life saver!"
category: tip
tags:
  - docker
  - docker-machine
  - networking
---
**Update:**

[docker-machine-ipconfig](https://github.com/fivestars/docker-machine-ipconfig) builds on the approach
I outline below, providing a more complete solution. In addition to setting the IP, it also disables
the DHCP service running on the docker machine and fixes-up the certificates for you.

***

If you run multiple docker machines for different projects, you might find problems due to the
dynamic assignments of IPs on startup.

Here's a little-known trick to stop that happening.

Start up your machine, I'm using `default` as an example, and issue the following command:

```
echo "ifconfig eth1 192.168.99.100 netmask 255.255.255.0 broadcast 192.168.99.255 up" | docker-machine ssh default sudo tee /var/lib/boot2docker/bootsync.sh > /dev/null
```

Here I'm fixing `default`'s IP to `192.168.99.100`. Stop, then start the machine, and it should be allocated
the correct IP.

Now let's create a new `testy-mctestface` machine:

```
docker-machine create testy-mctestface --driver virtualbox --virtualbox-memory 4096 --virtualbox-disk-size 50000
```

Here I'm creating it with 4GB of memory and a 50Gb drive.

Start that machine up, and issue the following:

```
echo "ifconfig eth1 192.168.99.150 netmask 255.255.255.0 broadcast 192.168.99.255 up" | docker-machine ssh testy-mctestface sudo tee /var/lib/boot2docker/bootsync.sh > /dev/null
```

I'm assigning the IP `192.168.99.150` to this machine. Stop, start, and the run the following:

```
docker-machine regenerate-certs testy-mctestface 
```

To regenerate the certs, something docker would complain about if you ran 
`docker-machine env testy-mctestface`.

Stop and start the machine one final time, and run `docker-machine ls` -- you should see your
new machine listed, with it's correct IP, and there shouldn't be any errors in the far-right column.

***

This trick will allow you to set up custom `/etc/hosts` entries for your machines without having to 
worry about the IPs changing all the time.

Happy coding!
