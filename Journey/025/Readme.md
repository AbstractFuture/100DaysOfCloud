# LFCS Exam Review pt8

## Introduction

Today I continued with the LFCS practice. I covered LVM, creating encrypting disks with cryptsetup, fdisk vs gdisk, mkswap, and fstrim.

## Prerequisite

I used a CentOS 7 VM. Steps or explanations may differ on other distros.

## LVM

Logical Volume Management exists because as the free space on your partitions decreases and aproaches zero, you need to create volumes from several partitions that may even span several different disks. 

The LVM utility and its' related commands like lvcreate are used to do so.

## cryptsetup

While using this utility on a new partition, I ran in to an error. It said it ```failed to setup dm-crypt key mapping for device``` and after checking the journalctl logs I saw an ```unknown target type``` error. 

To add a bit of context, the utility started, seemed to work fine (I successfully chose a target disk and also selected a password) but as I finished retyping the password the utility would fail. 

The tutorial I was watching didn't have this error at all! 

I decided to try simple trouble shooting ideas: were all my packages up to date? I hadn't considered that was the issue, but I figured it was a good start. I updated all packages with ```yum``` and used the cryptsetup utility once more, this time successfully! 

## fdisk vs gdisk

fdisk and gdisk are both utlities that manipulate partitions (create, delete, etc.) but fdisk has a limit of 5 partitions and up to 2T whereas gdisk can handle up to 128 primary partitions.

I intend to use gdisk and not fdisk during the LFCS so I can focus on problem solving the exam questions and not worrying about the limitations of the utility.

## mkswap

Like ```mkfs```, we use ```mkswap``` instead of ```mkfs``` when setting up our swap partition and this tells linux that it is intended to be a swap as opposed to file systems like xfs or ext4.

## fstrim

```fstrim``` is a utility designed to clean up and optimize ssd storage media. You automate it so it runs weekly (less room for forgetfulness/ human error).

I used a one-off command for the purposes of my testing as opposed to full weekly automation.

```
# systemctl enable --now fstrim.timer
```

## Next Steps

I intend to continue studying for my (rapidly approaching) exam on Friday Sept. 7th. Wish me luck!

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1300238091035324422)
