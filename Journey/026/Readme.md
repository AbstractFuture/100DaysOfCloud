# LFCS Exam Review pt9

## Introduction

I reviewed some basic linux time and date related commands. I don't expect the LFCS to focus on these commands too much but they're good to know. 

If you have booked your exam and you have a limited amount of time to study it would be worthwhile to focus on LVM, containers, and creating and managing users, groups, and permissions related to users and groups. 

## Prerequisite

A VM. I used a CentOS 7 VM for this exercise.

## Cloud Research

Here is an overview of the related commands.

```timedatectl``` will be the main way to interact with altering your settings. For an overview of your time settings use:
```
# timedatectl status
```
You can use --help, man pages or auto complete to see what options are available for ```timedatectl```.

For example, using tab auto complete I see the ```set-timezone``` option available. I'll use tab auto complete once more and see that before it prints out all 400+ timezones, it asks me to confirm if it wants me to do that. I appreciate that it doesn't automatically dump all those lines onto my terminal.

An example of using ```set-timezone``` is shown below:
```
# timedatectl set-timezone America/Los_Angeles
```
After executing that you'll see your timezone has changed right away with no need to reboot.

```hwclock``` is the tool to manage hardware time. Hard ware time is the time related to the physical device, and is on the BIOS.  

```NTP``` stands for Network Time Protocol. Perhaps the most important part of NTP is understanding the concept of stratum. Stratum indicates the reliability of the server you are syncing your time with.

Stratum 1 is the highest level of reliability - these are clocks synced to an atomic clock.

Stratum 10 means server is not taking part in any synchronization and stratum 16 means dont use this stratum, something is wrong.

The remaining numbers between 1-16 that were not listed indicate how reliable the sync is compared to stratum 1. 

"Insane clock" is a concept where the clock you are attempting to sync to is too different from your ntp client's time and it won't allow the sync to occur. You will need to adjust your hardware time in this instance before syncing.

```iburst``` tells the ntp client to ignore insane clock.

```chronyc``` chronyc is the redhat process that takes care of ntp.
```chronyc sources``` shows which ntp stratums you are using.

```ntpdate``` allows you to set date from the ntp server and ```ntpdate pool.ntp.org``` specifically allows you to fetch time from ntp server from ntp.org right now. It is a convenient way to fix an urgent time problem.

```ntpq``` allows you to query ntp.

## Try yourself

You now have the information to complete the following tasks.

### Task 1

View the current time properties on your server.

### Task 2

Synchronize with an ntp server at this moment.

## ☁️ Cloud Outcome

You can now see and alter time settings on your system.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1300424509779070976)
