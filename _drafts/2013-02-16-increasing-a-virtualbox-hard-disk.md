---
layout: post
title: "Increasing a VirtualBox hard-disk"
excerpt: "Use slax, don't forget to create an iso with gpart"
tags: 
- development
- virtualbox
- linux
published: true
---

<p>Use <a href="http://slax.org" target="_blank">slax</a>, don't forget to create an iso with gparted as part of the bundle.</p>

<blockquote><pre>
dd -if= -of=
</pre></blockquote>

<p>Use gparted to convert the unused disk space into a usable disk, formatted as ext3.</p>

<p>Use the LVM management commands to create a physical volume, link that to a volume group, then extend your logical volume over the new space.</p>

<blockquote><pre>
~# lvmdiskscan /dev/hda2
  /dev/VolGroup00/LogVol00 [       3.97 GB]
  /dev/hda1                [     101.94 MB]
  /dev/VolGroup00/LogVol01 [     512.00 MB]
  /dev/hda2                [       4.50 GB] LVM physical volume
  
~# umount /dev/hda3
~# pvcreate /dev/hda3
  Physical volume "/dev/hda3" successfully created
~# vgextend VolGroup00 /dev/hda3
  Volume group "VolGroup00" successfully extended
~# lvextend -L+5GB /dev/VolGroup00/LogVol00 /dev/hda3
  Extending logical volume LogVol00 to 8.97 GB
  Logical volume LogVol00 successfully resized
~# e2fsck -f /dev/VolGroup00/LogVol00
e2fsck 1.41.3

Do you really want to continue (y/n)? yes

Adding dirhash hint to filesystem.

Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

/dev/VolGroup00/LogVol00: ***** FILE SYSTEM WAS MODIFIED *****
/dev/VolGroup00/LogVol00: 159006/1040384 files (2.0% non-contiguous), 952672/1040384 blocks
~# resize2fs /dev/VolGroup00/LogVol00
resize2fs 1.41.3
Resizing the filesystem on /dev/VolGroup00/LogVol00 to 2351104 (4k) blocks.
The filesystem on /dev/VolGroup00/LogVol00 is now 2351104 blocks long.

</pre></blockquote>

<p>Reboot, and you're done.</p>
