# LFCS Exam Review pt5

## Introduction

Today I reviewed commands for storage management. 

## Prerequisite

A CentOS 7 VM is preffered as there are some differences in procedure between fdisk and gdisk (the Ubuntu default command). But I always encourage expirimentation so once you have a grasp of this on CentOS 7 feel free to try to reproduce these steps on Ubuntu.

## Cloud Research

I will include excerpts of the command descriptions from their man pages.

lsblk
```
NAME
       lsblk - list block devices

SYNOPSIS
       lsblk [options] [device...]

DESCRIPTION
       lsblk  lists  information  about  all  available or the specified block
       devices.  The lsblk command reads the sysfs filesystem and udev  db  to
       gather  information.  If  the udev db is not available or lsblk is com‐
       piled without udev support than it tries  to  read  LABELs,  UUIDs  and
       filesystem  types  from the block device. In this case root permissions
       are necessary.
```
fdisk (the mbr utility) - I used this command to create a new partition. 
```
NAME
       fdisk - manipulate disk partition table

SYNOPSIS
       fdisk [options] device

       fdisk -l [device...]

DESCRIPTION
       fdisk  is a dialog-driven program for creation and manipulation of par‐
       tition tables.  It understands GPT, MBR, Sun,  SGI  and  BSD  partition
       tables.

```
partprobe - After creating the partition I was prompted to use ```partprobe``` to tell the kernel to check for a new partition. Entering ```partprobe``` without any options was sufficient.
```
NAME
       partprobe - inform the OS of partition table changes

SYNOPSIS
       partprobe [-d] [-s] [devices...]

DESCRIPTION
       This manual page documents briefly the partprobe command.

       partprobe is a program that informs the operating system kernel of partition table changes.

```
mkfs - I chose to make my new partition a .xfs file system (the default for redhat). 
```
NAME
       mkfs - build a Linux filesystem

SYNOPSIS
       mkfs [options] [-t type] [fs-options] device [size]

DESCRIPTION
       This mkfs frontend is deprecated in favour of filesystem specific mkfs.<type> utils.

       mkfs  is  used to build a Linux filesystem on a device, usually a hard disk partition.  The device
       argument is either the device name (e.g.  /dev/hda1, /dev/sdb2), or a regular file that shall con‐
       tain the filesystem.  The size argument is the number of blocks to be used for the filesystem.

       The exit code returned by mkfs is 0 on success and 1 on failure.

       In  actuality, mkfs is simply a front-end for the various filesystem builders (mkfs.fstype) avail‐
       able under Linux.  The filesystem-specific builder is searched for via your PATH environment  set‐
       ting only.  Please see the filesystem-specific builder manual pages for further details.
```
mount - I used this command to mount the filesystem to /mnt
```
NAME
       mount - mount a filesystem

SYNOPSIS
       mount [-l|-h|-V]

       mount -a [-fFnrsvw] [-t fstype] [-O optlist]

       mount [-fnrsvw] [-o options] device|dir

       mount [-fnrsvw] [-t fstype] [-o options] device dir

DESCRIPTION
       All  files accessible in a Unix system are arranged in one big tree, the file hierarchy, rooted at
       /.  These files can be spread out over several devices.  The mount command serves  to  attach  the
       filesystem  found  on  some  device  to the big file tree.  Conversely, the umount(8) command will
       detach it again.  The filesystem is used to control how data is stored on the device  or  provided
       in a virtual way by network or another services.

       The standard form of the mount command is:

              mount -t type device dir

```
findmnt - while I did not need this command in this simple exercise, I imagine that it can be useful with more complicated tasks. 
```
NAME
       findmnt - find a filesystem

SYNOPSIS
       findmnt [options]

       findmnt [options] device|mountpoint

       findmnt [options] [--source] device [--target|--mountpoint] mountpoint

DESCRIPTION
       findmnt will list all mounted filesystems or search for a filesystem.  The findmnt command is able
       to search in /etc/fstab, /etc/mtab or /proc/self/mountinfo.  If device or mountpoint is not given,
       all filesystems are shown.

       The device may be specified by device name, major:minor numbers, filesystem label or UUID, or par‐
       tition label or UUID.  Note that findmnt follows mount(8) behavior where  a  device  name  may  be
       interpreted as a mountpoint (and vice versa) if the --target, --mountpoint or --source options are
       not specified.

       The command prints all mounted filesystems in the tree-like format by default.

```
umount - I ended the exercise with unmounting the partition from /mnt. I entered ```umount /path/to/partition``` without any options to successfully unmount. 
```
NAME
       umount - unmount file systems

SYNOPSIS
       umount -a [-dflnrv] [-t fstype] [-O option...]

       umount [-dflnrv] {directory|device}...

       umount -h|-V

DESCRIPTION
       The  umount  command detaches the mentioned file system(s) from the file hierarchy.  A file system
       is specified by giving the directory where it has been mounted.   Giving  the  special  device  on
       which  the  file  system lives may also work, but is obsolete, mainly because it will fail in case
       this device was mounted on more than one directory.

       Note that a file system cannot be unmounted when it is 'busy' - for example, when there  are  open
       files on it, or when some process has its working directory there, or when a swap file on it is in
       use.  The offending process could even be umount itself - it opens libc, and libc in its turn  may
       open for example locale files.  A lazy unmount avoids this problem.

```
lsof - This command can be used for trouble shooting. If you get an error while trying to unmount a partition that specifies that the partition is in use; lsof can give you hints as to why. It will list all open files. Sometimes the reason it won't unmount is simple (like being in the directory you are trying to unmount) or sometimes it will be more obscure and you will need to investigate further.
```
NAME
       lsof - list open files

SYNOPSIS
       lsof [ -?abChKlnNOPRtUvVX ] [ -A A ] [ -c c ] [ +c c ] [ +|-d d ] [ +|-D D ] [ +|-e s ] [ +|-E ] [
       +|-f [cfgGn] ] [ -F [f] ] [ -g [s] ] [ -i [i] ] [ -k k ] [ +|-L [l] ] [ +|-m m ] [ +|-M ] [ -o [o]
       ] [ -p s ] [ +|-r [t[m<fmt>]] ] [ -s [p:s] ] [ -S [t] ] [ -T [t] ] [ -u s ] [ +|-w ] [ -x [fl] ] [
       -z [z] ] [ -Z [Z] ] [ -- ] [names]

DESCRIPTION
       Lsof revision 4.89 lists on its standard output file information about files opened  by  processes
       for the following UNIX dialects:

            Apple Darwin 9 and Mac OS X 10.[567]
            FreeBSD 8.[234], 9.0, 10.0 and 11.0 for AMD64-based systems
            Linux 2.1.72 and above for x86-based systems
            Solaris 9, 10 and 11
```

## Social Proof

[Tweet]()
