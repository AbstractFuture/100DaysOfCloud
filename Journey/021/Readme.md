# LFCS Exam Review pt4

## Introduction

Today I learned about sticky bit permissions.

## Prerequisite

I specifically used a CentOS 7 VM but I imagine most (or all) distros have standardized permission commands/ tools so feel free to expiriment on your prefferred distro :)

## Use Case

Imagine this: A user responsible for their own department as well as other departments may warrant a different level of access than a user lower in the heirarchy. For example, this person may want to be able to see what files exist in the other department directories, but users in these departments may not need to have access (either writing or deleting) to another departments files. 

This is where sticky bit comes in.

## Cloud Research

From the chmod man page:

```
RESTRICTED DELETION FLAG OR STICKY BIT
       The  restricted  deletion  flag  or  sticky  bit is a single bit, whose
       interpretation depends on the file type.  For directories, it  prevents
       unprivileged  users  from  removing or renaming a file in the directory
       unless they  own  the  file  or  the  directory;  this  is  called  the
       restricted  deletion  flag  for the directory, and is commonly found on
       world-writable directories like /tmp.  For regular files on some  older
       systems,  the  bit saves the program's text image on the swap device so
       it will load more quickly when run; this is called the sticky bit.
```

## Try yourself

For this example I have the following directories already set up:

```
[root@centos]# ll /permpractice/
total 8
drwxrwx--- 2 boss account 4096 Aug 23 08:51 account
drwxrwx--- 2 boss sales   4096 Aug 23 08:51 sales
```

These are 2 different departments directories both with their own group ID, and the boss needs to be able to delete files in the account directory even when belonging to the sales group. 

I use the following command to enable the boss user to do so and then verify that the permissions have changed:

```
[root@centos]# chmod +t account
[root@centos]# chmod +t sales
[root@centos]# ll /permpractice/
total 8
drwxrwx--T 2 boss account 4096 Aug 23 08:51 account
drwxrwx--T 2 boss sales   4096 Aug 23 08:51 sales
```
Notice the capital 'T' indicating sticky bit permissions are in effect.

## Next Steps

Continue studying for my rapidly approaching LFCS exam! I still need to cover managing storage, networking, containers, more practice managing services, and automating tasks.

## Social Proof

[Tweet]()
