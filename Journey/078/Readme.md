
# LVM, RAID, QUOTA, SSH & Other Labs

## Introduction

Today I worked through creating logical volumes, RAID solutions, implementing user quotas on both ext4 and xfs filesystems, some ssh practice as well as command review and timed lab speedrun of all previous labs. I still need more practice regarding SELinux and iptables (not sure why I found these to be the least intuitive subjects).

## Prerequisite

A CentOS 7 VM. 

### LVM topics

I practiced creating physical volumes, volume groups (which rely on having physical volumes available to them), and logical volumes (which rely on storage in the volume group). 

I also worked on extending or reducing the logical volume size. I should note that it is recommended to resize both the filesystem and logical volume in a single command, otherwise you risk data corruption. 

### RAID solutions

I added a virtual disk to my VM for practice purposes. I created both RAID 1 and RAID 5 devices.

I practice failing, removing, and replacing a device in the RAID 5 configuration, as well as mounting RAID devices persistently. 

### SSH

I setup an ssh connection to a virtual machine and also practiced setting up a passwordless ssh setup on kodekloud such that I could ssh into a remote machine without ever being prompted for a password.

## Next Steps

- Complete another lab speedrun covering the labs mentioned here

- Complete web, ftp, DNS, and SAMBA labs. 

## Social Proof

[Tweet]()
