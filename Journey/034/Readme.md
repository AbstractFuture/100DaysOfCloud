# LFCS Exam Review pt17

## Introduction to RAID level 5

My understanding of RAID (which consist of many different levels/configurations) is based on what I think would be needed to know for the LFCS.

My lab and study materials focus on level 5 so this article will do so as well.

I'll take you through the commands I used as well as the setup of my virtual machine.

## Prerequisite

A CentOS 7 VM.

## Use Case

A level 5 RAID solution is a collection of block devices or partitions that, in the event of one block device/ partition failing, the RAID setup will swap the failed drive for the spare drive, and then write the information to the new drive, keeping your data intact. Pretty neat, right?

I'm sure there are specific use cases for different raid levels (which is beyond the scope of this article) so if this interests you I definitely encourage you to keep learning! 

## Cloud Research

Since this level 5 RAID setup uses multiple block device partitions, I created 4 additional Virtual Hard disks with 1.5G space per disk in the storage configuration of my Oracle VM Virtualbox Manager before actually booting up my VM.

Originally I intended to make each block device a single gigabyte, but I wasn't sure if during the setup using gdisk, the raid setup, and putting a filesystem on there, would reduce the available space to less than 1GB. So to be safe I created a single partition on each of these new block devices that were 1GB in size. I have not yet tested if that was necessary or not.

## Try yourself

Firstly, check your block devices to ensure you've adjusted your VM settings correctly.

```
$ lsblk
```
I see the additional block devices available so I am good to proceed. 

Next, using gdisk, I create a new 1GB partition and chose the 'linux raid' code so that I can later use the partition in my RAID setup. I repeat this process for each new block device I added.

After confirming that each new block device has a partition, we can use the ```mdadm``` utility (used for managing linux raid software) to create our level 5 setup.

```
$ mdadm --create /dev/md0 --level=5 --raid-disks=3 -spare-disks=1 /dev/sdd1 /dev/sde1 /dev/sdf1 /dev/sdg1
```

Depending on how many block devices you had prior to this lab, your specific block device names will be different. 

The above command tells ```mdadm``` to create a multiple disk device (md0), that this setup is a level 5 raid configuration, and that that it has 3 main disks and one spare that will take the place of the failed disk.

```mdadm``` also allows us to swap out faulty disks or add new disks which is very convenient. It would be inconvenient to engineer this utility such that you're required to move all data from the disks to a totally new raid setup after one fails.

Anyways, on with the walkthrough:

```
$ mdadm --detail /dev/md0
```

Specify which multiple disk raid setup you want more information on with the   ```--detail``` option and it will display the status of all devices/partitions in the raid setup as being faulty or active.

You can actually practice changing block devices in this setup by using ```--fail``` and specifying which block device/partition to fail. 

```
$ mdadm /dev/md0 --fail /dev/sdf1
```
Verify what has happened to the now failed disk, as well as the spare.
```
$ mdadm --detail /dev/md0
```

You should see the specified disk now set to faulty, and that the spare disk is now in use! Then remove the faulty disk and add a new one (you will need a block device/ partition that is formatted such that it can be used as a raid device first!).

```
$ mdadm /dev/md0 --remove /dev/sdf1
$ mdadm /dev/md0 --add /dev/sdh1
```
In theory, since you used the ```--fail``` option on /dev/sdf1, and there's actually nothing wrong with the hardware, we could add it back into the raid setup with the ```--add``` option. However I have not yet tested this out with my configuration. If your disk was physically damaged you would not be adding it back in. 

## ☁️ Cloud Outcome

You've now setup a RAID 5 solution! Congrats!

## Next Steps

User Quotas and SSH stuff will likely be my next focus. 

## Social Proof

[Tweet]()
