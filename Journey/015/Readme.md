
# GRUB & Quiet  

## Introduction

✍GRUB stands for Grand Unified Bootloader which is a bootloader package that lets you choose to boot from multiple operating systems installed on the computer. 

"Quiet" in this case refers to a setting I intend to change in the default grub settings. 

## Prerequisite

This demonstration will be on a CentOS7 VM. Grub file locations may differ among other distros so keep that in mind if you intend to follow along.

## Use Case

If you want to see all standard boot messages displayed (for troubleshooting purposes or out of curiousity) then you'll need to alter the default settings located in ```/etc/default/grub```.

## Try yourself

### The Default File

The default settings look like this in CentOS 7:
```
GRUB_TIMEOUT=5
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
```

### The Changes To The Default File

Notice "```rhgb quiet```". This supresses messages from being displayed when booting up. Simply delete that so the file looks like so:

```
GRUB_TIMEOUT=5
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="crashkernel=auto"
GRUB_DISABLE_RECOVERY="true"
```
Save and exit. Remember that everything in linux is a plain text file, so we need to tell our system to check this file again and make the appropriate changes.

```
[root@centos ~]# grub2-mkconfig -o /boot/grub2/grub.cfg
```

Once that is done you need to reboot, and then you're good to go!


## Links For More Info

[GNU GRUB](https://en.wikipedia.org/wiki/GNU_GRUB)

[Setting Up grub2 On CentOS 7](https://wiki.centos.org/HowTos/Grub2)

## Social Proof

[Tweet]()
