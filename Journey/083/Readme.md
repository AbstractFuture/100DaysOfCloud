
# Samba Server & Quota speedrun

## Introduction

Today I (mostly) redid the Samba (and NFS, but mostly Samba) server lab and mounted it persistently on a remote machine. I also tried redoing the quotas on both xfs and ext4 filesystems and realized I need more practice. 

## Prerequisite

2 CentOS7 VMs. And some patience.

## Cloud Research

### SAMBA/NFS

I mainly spent the most of the time in this lab troubleshooting a mount error on the remote machine. I tried restarting samba on both machines, verified the firewall configuration on both machines, and made sure that the server was indeed available on a remote machine.

HOWEVER, what I forgot to do was create a linux user on the second machine that would match the credentials entered on the first machine with ```smbpasswd -a < usernamegoeshere >```. A rookie mistake. 

### Quota Speedrun

I can tell I'll need to redo this lab another 2-3 times before I can recall all the commands. 

ext4 and xfs filesystems use different commands to create quotas and enforce them. It's clear I should be redoing this lab at least once a day until I can recall all commands with proper syntax.

### Other Labs

I also configured logrotation, rsyslog, made journald persistent, and some minor cron labs.

## Next Steps

- do quota lab at least once per day
- review RAID labs (creating different kinds of RAID configurations from scratch)
- virtual hosts labs (until I can perform it faster)
- get faster with SELinux
- firewalls
- LVM (and extending or reducing a logical volume)
- crypttab labs
- configuring ftp services
- mail
- creating a caching only DNS (also some other related DNS stuff)
- Databases (mariadb)
- some containerization, although I'm very comfortable with it now
- some network review
- and lastly, doing some web proxy labs and restricting access using squid

## Social Proof

[Tweet]()
