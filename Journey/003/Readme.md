

# inodes & Symbolic Links

## Introduction

I'll be taking the LFCS exam shortly (Linux Foundation Certified Sysadmin) and one of the practice exam tasks was about creating both hard and symbolic links to files, while inodes are a component in linux computing that stores the information about a file.

## Prerequisite

This will be a fairly basic overview for a basic topic, so the only prerequisites are a willingness to learn and a real good attitude! If you've got both of those - you're off to a good start.

## Use Case

Files or directories may be moved to disks with more space but in doing so you may break your scripts that point to a file/directory that is no longer there. 


## Try yourself

So let's go over where you'll see the inode information and how we can use it to verify that a hard or symbolic link has been created.

### Seeing The inode Information

We start with a simple listing of (any) directory and specify we want to see the inode information.
```
ls -li
```
Output is as follows:
```
total 729564
18481589 drwxr-xr-x 12 steven steven      4096 Jun 11 09:08  anaconda3
18365556 -rwx------  1 steven steven 425991075 Jan 30  2017  Anaconda3-4.1.1-Linux-x86_64.sh
18616766 drwxr-xr-x  2 steven steven      4096 Jun 11 08:14  certs
 4980788 -rw-rw-r--  1 steven steven  63476994 Aug  2 22:23  code_1.47.3-1595520028_amd64.deb
18350150 drwxr-xr-x  7 steven steven      4096 Aug  2 22:19  Desktop
18350154 drwxr-xr-x  3 steven steven      4096 Jul 19 16:57  Documents
18350151 drwxr-xr-x  2 steven steven      4096 Aug  2 22:25  Downloads
18350084 -rw-r--r--  1 steven steven      8980 Jun  7 19:27  examples.desktop
18481253 drwxrwxr-x  8 steven steven      4096 Jun 29 22:35  idea-IC-201.7846.76
20185592 drwxr-xr-x  3 steven steven      4096 Jul  1 11:56  IdeaProjects
18351824 lrwxrwxrwx  1 steven steven        11 Jun 21 11:33  init.d -> /etc/init.d
18481346 drwxr-xr-x  7 steven steven      4096 Mar 12 03:05  jdk1.8.0_251
 4849723 -rw-rw-r--  1 steven steven 195662801 Jun 30 08:41  jdk-8u251-linux-i586.tar.gz
20186808 drwxr-xr-x  8 steven steven      4096 Jun 23 22:21  kafka_2.12-2.5.0
 4849729 -rw-rw-r--  1 steven steven  61604633 Jun 23 21:52  kafka_2.12-2.5.0.tgz
18353686 -rw-r--r--  1 steven steven    234721 Jul  5 18:02  lf.html
18350155 drwxr-xr-x  2 steven steven      4096 Jun  7 19:32  Music
18350156 drwxr-xr-x  2 steven steven      4096 Jul 19 09:54  Pictures
18350153 drwxr-xr-x  2 steven steven      4096 Jun  7 19:32  Public
18350445 drwxr-xr-x  8 steven steven      4096 Jul  5 18:19  snap
18356185 -rw-r--r--  1 steven steven         0 Jul  1 11:56  stale_outputs_checked
18350152 drwxr-xr-x  2 steven steven      4096 Jun 14 20:50  Templates
20185604 drwxr-xr-x  2 steven steven      4096 Jun  1 11:40  Ubuntu-18-04
18350157 drwxr-xr-x  2 steven steven      4096 Jun  7 19:32  Videos
20709386 drwxrwxr-x  4 steven steven      4096 Aug  3 14:10 'VirtualBox VMs'
```

The first field is the inode number. Each file will have a unique inode number. You can create several hard links that point to the same inode or you can create a symbolic link that points to a name of a hard link.

### Creating A Hard Link


From the man ln page:
```
NAME
       ln - make links between files

SYNOPSIS
       ln [OPTION]... [-T] TARGET LINK_NAME   (1st form)
```

So let's try creating a hard link for an existing file in my home directory and comparing the two inode numbers to verify that they both point tothe same inode (and the inode points to blocks on disk).

```
ln lf.html linuxfoundationhtml
ls -li lf.html linuxfoundationhtml
```
Output:
```
18353686 -rw-r--r-- 2 steven steven 234721 Jul  5 18:02 lf.html
18353686 -rw-r--r-- 2 steven steven 234721 Jul  5 18:02 linuxfoundationhtml
```
We've confirmed that both inodes are the same, which mean these links are identical to the blocks on disk. 

Now let's create a symbolic link and compare that to our original file and to our new hard link.

```
ln -s ~/linuxfoundationhtml ~/symlink
ls -li lf.html linuxfoundationhtml symlink
```
Output:
```
18353686 -rw-r--r-- 2 steven steven 234721 Jul  5 18:02 lf.html
18353686 -rw-r--r-- 2 steven steven 234721 Jul  5 18:02 linuxfoundationhtml
18353690 lrwxrwxrwx 1 steven steven     32 Aug  6 11:09 symlink -> /home/steven/linuxfoundationhtml

```

Firstly you'll notice that symlink has a different inode number (because it isn't pointing to blocks on disk, it is pointing to a hard link that points to an inode number that points to blocks on disk - a real tongue twister).

Secondly you should notice that the file size for our symbolic is much smaller than the original file and that is because a symbolic link only neds to point to the name of the file location we specified. 


## ☁️ Cloud Outcome

While testing this out I learned that hard links do not work for directories but symbolic links do! 

## Next Steps

I'll continue creating content around studying for the LFCS and CKA and other things.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1291398149756669952)
