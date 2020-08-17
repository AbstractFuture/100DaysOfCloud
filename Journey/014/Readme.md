# Linux Kernel Module Commands

I'll list a few basic commands, what they do, why I use them, and how to perform some basic tasks.

## Introduction

We'll determine which Linux kernel modules are currently loaded in our system, load the module for vfat support, determine if the vfat support module has any dependencies, unload this module, and ensure that our system can be used to forward IP packets.

## Prerequisite

A CentOS 7 VM. 

## List Of Linux Kernel Modules

Open up terminal and use 

```
[root@centos ~]# lsmod
```
to determine which modules are loaded.

The rightmost column for this output, titled 'used by' provides information about dependencies. 

## Load VFAT Module

To manually load a kernel module, specifically vfat, use the following command:

```
[root@centos ~]# modprobe vfat
```
Now reuse the previous command in the following way to confirm that the vfat kernel module was loaded:

```
[root@centos ~]# lsmod | grep vfat
vfat            17461   0
fat             65950   1   vfat
```

The output in the rightmost column indicates that ```fat``` is a dependency of ```vfat```. 

## Unload A Module

```
[root@centos ~]# modprobe -r vfat
[root@centos ~]# lsmod | grep vfat
[root@centos ~]# 
[root@centos ~]# lsmod | grep fat
[root@centos ~]# 
```
No results found for vfat or fat indicates we've successfully unloaded the module. I should note that modprobe considers dependencies which is why I only needed to remove vfat with a single command instead of removing vfat and then using ```modprobe -r fat```. 

## Forwarding IP Packets

Find the setting that indicates if IP forwarding is enabled:
```
[root@centos ~]# sysctl -a | grep 'net.ipv4.ip_forward ='
net.ipv4.ip_forward = 0
```
Zero indicates the setting is disabled. In order to enable we need to edit the sysctl.conf file.

```
[root@centos ~]# nano /etc/sysctl.conf
```
And paste the following line at the bottom of the config file:

```
net.ipv4.ip_forward = 1
```
Save and exit the conf file. 

Now that we've enabled IP forwarding, our server will behave like a router.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1295343927969624064)
