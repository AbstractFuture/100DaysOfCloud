

# Basic Linux Permissions (& VM troubleshooting)

## Introduction

Today I focused on completing basic user creation and file/directory permissions.

I also needed to remove and recreate my centos VM because after enabling the embedded virtualization option on that machine my Ubuntu desktop began freezing often. I've read that this may also have been from firefox updates but I do not intend to A/B test between the two. 

In any case I have a fresh CentOS 7 VM to complete my labs on.

## Prerequisite

A CentOS 7 VM.

## Use Case

The idea in this lab was to set up a set of directories and alter the owner and group membership so that managers in those departments could read write and execute, while other department staff would be unable to view or edit the directory contents. 

## Cloud Research

For the purposes of the LFCS, I recommend to read through the entire question first. For example, the task may not be listed in the optimal order such as creating users and assigning users to groups. Instead you should create the groups first and then in a single line of code assign the group to the user during user creation. 


I should also note that it only makes sense to begin creating users if the LFCS task doesn't mention altering default settings (which I find unlikely). Take your favourite text editor and alter the contents of ```/etc/login.defs``` such that you are complying with the task. 

```/etc/login.defs``` is a file that will contain information like how many days a password will be valid for, and much more!

It is also important to note that during user creation by default on CentOS a user will get a home directory. Your system will replicate the contents of ```/etc/skel``` so if the task mentions that a home directory ought to have new default files - its a strong hint to go into ```/etc/skel``` and create files in accordance with the task.

If the task doesn't require changes to  ```/etc/login.defs``` or ```/etc/skel``` then you can get right into creating new groups and users;

```
$ groupadd examplegroup
$ groups # confirming the group creation was successful
```
Next, in a single line, create a user and make them a part of the examplegroup.

```
$ useradd -G examplegroup newusernamegoeshere
$ id newusernamegoeshere # confirming that they have the group assigned to them
```

## Next Steps

I intend to:

- recall and implement docker and lxc commands from the previous few days
- create a new VM and setup users and permissions and directories from scratch (practice makes perfect!)
- redo labs related to storage like LVM and RAID

## Social Proof

[Tweet]()