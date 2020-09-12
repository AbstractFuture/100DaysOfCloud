# LFCS Exam Review pt18

## Introduction To User Quotas

User quotas are what they sound like. They are quotas on the soft or hard limits of bytes of information that a user can write on a specific filesystem.

## Prerequisite

A CentOS 7 VM and either an ext4 or xfs filesystem.

## Use Case

A soft limit allows the user to exceed the limit but will need to delete other files on the filesystem within a grace period (usually a week).

A hard limit will not allow the user to exceed the byte limit at all.

Limits help control what a user can do and reduces the vulnerability of your system to malicous attacks or insecure practices.

## Cloud Research

I personally found this topic simple for ext4 filesystems but I found it harder to recall the commands or procedure for xfs.

Since I'm still learning I don't think I'll create a tutorial, but I will leave an exercise for the reader to complete if they feel so inclined.

### ext4 filesystem user quotas

You will need to verify if you already have the ```quota``` package installed. It is not available by default on some distros. 

```
$ which quota
```

If no package is found then download it:
```
$ sudo yum install -y quota
```
After downloading, we need to alter the ```/etc/fstab/``` remount the altered filesystem with read and write permissions, confirm that everything was mounted correctly, and then create user specific quota files before turning quota on.

With your favourite text editor, replace the ```defaults``` option in ```/etc/fstab``` with ```usrquota,grpquota``` as I have typed it. No spaced needed. 

Unmount the filesystem and then remount it with read and write permissions. Mount all filesystems so that you will be alerted to any issues with mounting. This helps us reduce troubleshooting time later if we are unsuccessful for any reason. It helps us remove a layer of ambiguity.

```edquota``` will allow you to specify a user name, create a quota configuration file where you can specify hard and soft limits, and then save and exit. I recommend checking out the ```edquota``` man pages for more details like syntax and options. 

```quotacheck``` will check quotas for users, groups, files, directories, etc based on the options you specify. This is a good way to see if you have any quota configurations saved on the filesystem.

Once that is verified to work, go ahead and and use ```quotaon``` to enable quota. 

```repquota``` can be used to see a report of quota usage.

### xfs filesystem user quotas

xfs uses ```xfs_quota``` is the single command with many options for a sysadmin to manage user quotas.

Replace ```defaults``` in the ```/etc/fstab``` with ```uquota```. Next, remount the filesystem with read and write permission and then mount all filesystems to ensure that there aren't any errors. 

```
$ mount | grep xfs
```
Can be used to see if the device and confirm if ```usrquota``` is specified on the xfs filesystem. 

Unlike ```edquota``` which creates a config file, ```xfs_quota``` requires the sysadmin to pass a string with certain syntax specifying that the string is about limits, and then specifying the hard and soft limits as well as the user it is supposed to apply to. After that, specify the mount point.

An example:

```
$ xfs_quota -x -c 'limit bsoft=1024m bhard=1024m usernamegoeshere' /mountpoint
```

You can also use ```xfs_quota``` for a usage report:
```
$ xfs_quota -x -c report /mountpoint
```

I recommend checking out the ```xfs_quota``` man page for yourself for a full list of options and uses. 

## Try yourself

Create a new user and asign a soft and hard limit of 1GB on an ext4 filesystem as well as an xfs system. Login as the new user and try using the following command to copy over a file that will exceed the hard and soft limits set on the filesystem. Adjust the output file path as necessary.

```
$ dd if=/dev/zero of=/filesystem/path/goes/here/lol
```

If after executing the command the ```dd``` process is halted due to exceeding limits (check the error message to confirm this is the case and not an unrelated coincidence) then you have successfully set and enabled user quotas. Way to go!

## Next Steps

Reviewing labs around SSH, configuring web services, and FTP services.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1304606842568482816)
