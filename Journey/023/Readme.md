# LFCS Exam Review pt6

## Introduction

Today I reviewed networking. I reviewed NetworkManager, the network service, network configuration file location, and nmtui (network manager text user interface).

I also ran into issues around the network service. I am unsure of whether this is due to my VM configuration or the system settings. For example, in some VM network configurations would result in ping being unable to locate google.com! Definitely not ideal. I'll play around with it a bit more but I intend to do review of other topics as well. 

## Prerequisite

This article focuses on a CentOS 7 VM. Steps may not be reproducible among other distros.

## Cloud Research

### NetworkManager
NetworkManager (which also happens to be the only systemd service that uses capitals in its name) is a tool used to manage the network card settings. On my system it is located in ```/etc/sysconfig/network-scripts```.

The file is titled ```ifcfg-ens33```. If you are comfortable with a text editor you can edit this file directly instead of using NetworkManager.

### nmtui
nmtui is the NetworkManager Text User Interface. It allows you to edit the network card file. It is unstable with some redhat versions so be wary of using it carelessly. 

Like NetworkManager, you don't need to use nmtui if you are comfortable with a text editor and want to edit the file directly.

### The Network Service
This service activates or deactivates network interfaces that are configured to start at boot time. 

In my exam prep, the tutorial shows that the network service by default should be running, but it failed to start on my system.

I had a look at which configuration files are in the directory:
```
[root@centos]# ls /etc/sysconfig/network-scripts/
ifcfg-ens33
ifcfg-lo
```
It is my understanding that virtualbox uses a different naming convention. When I want to see the name of my network with ```ip addr show``` it shows up as ```enp0s3```. 

I try to force load ifcfg-ens33 using:
```
[root@centos]# ifup /etc/sysconfig/network-scripts/ifcfg-ens33
```
However I get the following error message:

```
Error: Connection activation failed: No suitable device found for this connection (device enp0s3 not available because profile is not compatible with device (mismatching interface name))
```
I thought that perhaps copying the file, renaming it and altering it's contents to replace instances of ```ens33``` with ```enp0s3``` would suffice if I re run the command using this new ```ifcfg-enp0s3``` configuration but I then get a new error:

```
Error   : [/etc/sysconfig/network-scripts/ifup-eth] Device ens33 does not seem to be present, delaying initialization.
```

Now that was a surprise! Does this mean my VM doesn't even have the device that the network service is supposed to manage?

This has been a very frustrating point in the tutorial.

## ☁️ Cloud Outcome

Practice makes perfect. Repeating these commands and committing them to memory so I can pass this LFCS exam.

## Next Steps

I intend to move onto other areas like managing storage, memory, and containers.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1299508206893510656)
