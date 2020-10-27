
# Lab Review: Encrypted Partitions 

## Introduction

Today I reviewed the commands and process to create and persistently mount an encrypted partition.

## Prerequisite

A CentOS 7 vm. Add an additional block device to it such that you have a partition you can expiriment with.

## Try yourself

Once the additional block device is added, feel free to follow along.

List block devices to verify you have a new additional device that isn't on your root file system. 

```
# lsblk
```

In this example, since I started from a brand new setup, I'll be creating and manipulating the partition on /dev/sdb.

```
# gdisk /dev/sdb
```

Create a partition on this block device following the gdisk prompts. Select the default linux filesystem code.

```
# cryptsetup luksFormat /dev/sdb1
```

This will create the encryption layer on top of the partition and also delete all existing information on it. You will be prompted to create a password to access this encrypted partition. Follow the instructions as prompted. 

```
# cryptsetup luksOpen /dev/sdb1 secret
```

"secret" is the name for this encrypted partition I chose, but you can name it whatever you'd like.

View the secret device with;

```
# ls -l /dev/mapper
```

Now that I've used ```cryptsetup luksOpen``` I can place a filesystem on the encrypted partition.

```
# mkfs.xfs /dev/mapper/secret
```

Before mounting it persistently you should check to see if you can copy files into it as a test.

```
# mount /dev/mapper/secret /mnt
# cp /etc/hosts /mnt
# ls -l /mnt
```
If it looks good, then we can unmount it from /mnt and move onto mounting it persistently. 

I now close the access to the partition. I can only access the partition now if I have the correct password (and spoiler alert: you should have it since you made it). 
```
# cryptsetup luksClose
```

Unlike mounting other filesystems, we have an additional step when working with a luks encrypted partition. We need to alter the contents of ```/etc/crypttab``` and put the partition name (that we chose earlier) and the physical partition info as described by ```lsblk```.

To access the file;
```
# vim /etc/crypttab
```
File contents should look like:

```
secret    /dev/sdb1
```

And then mount persistently in ```/etc/fstab``` with the following syntax:

```
/dev/mapper/secret  /secret     xfs     defaults        0 0
```

Before rebooting, use:

```
# mount -a
```

To determine if eveyrthing was successful. If it gives you no errors or warnings, you should be good to reboot. During reboot you will be prompted for the password to access the encrypted device, otherwise it will not mount it.

It is not convenient, but security is never convenient. 

## Next Steps

Labs including: LVM, RAID, user quota, SSH, web services, FTP services, DNS, and SAMBA servers.

## Social Proof

[Tweet]()