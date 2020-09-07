# update_grub_zfs

Attempts to debug and fix issues with Ubuntu with grub and ZFS.

Repeatedly, update-grub is broken in ways which will make an Ubuntu unbootable
if you have ZFS as your root filesystem.

## Why Are You Doing This?

I have had so much great experience with ZFS on FreeBSD, and I wanted the same
in Linux, but it's just been so much pain.

In order to help both myself and others, I decided to try to fix this issue
with ZFS and Grub on Ubuntu because it doesn't seem like anyone else is doing
it.


## Why Not Use FreeBSD or Another Linux Distro if Ubuntu is Broken

Because it's not the Open Source way. 

Because this is my hobby.

Because Ubuntu is the most popular distro in many domains, and it's going to
need to start using ZFS as a root filesystem.

## Should I use ZFS as my Root Filesystem

No.

Unless you plan on helping to troubleshoot this issue, you are in for hours of pain even with this guide. 

Please save yourself the trouble and only use ZFS on other drives than root.

Feel free to use ZFS as root on FreeBSD as the support is far better.

## Characterizing the Bug

Install Ubuntu and use the standards installer to install ZFS root.

After a while of updating packages, especially the kernel, update-grub will get run. This will create a grub.cfg which will be completely unbootable because it will be devoid of actual kernels in it's menu entry section.

## Fixes

TODO

Document all the steps one has to perform in order to bring a system back from the dead.

## Initramfs

The next level of this bug after one has "fixed" grub is that you will still be
dropped into initramfs every single time you boot.

This is not as bad as the former bug because you can do the following to boot:

```
 $ zpool import -R /root rpool
 $ exit
```

This command will mount your ZFS root filesystem on /root and it will continue to boot normally.

I do not have a fix for this problem, work is ongoing.
