
# sudo visudo

## Introduction

While studying for the LFCS exam (linux foundation certified sysadmin exam) I found the file and command that allows a sysadmin to grant users sudo permissions in Ubuntu and CentOS. It is known as ```visudo```.

## Prerequisite

I recommend having both an Ubuntu VM and CentOS VM open to really get a feel for what's happening. The file lengths are different in each distribution.

## Use Case

You, as a sysadmin, will need to know which conventions your distro uses if you wish to grant sudo permissions to users.

## Cloud Research
From the visudo man page:
```
     visudo edits the sudoers file in a safe fashion, analogous to vipw(8).  visudo locks the
     sudoers file against multiple simultaneous edits, provides basic sanity checks, and checks
     for parse errors.  If the sudoers file is currently being edited you will receive a message
     to try again later.
```

## Try yourself

I highly recommend using a VM when epirimenting with commands/ features you have no experience with. I would hate for you to alter settings that you forgot about and either remove functionality (not just liumited to the sudo functionality) from users or groups, but do serious harm to your system. Remember kids - stay safe.

## Social Proof

[Tweet](link)
