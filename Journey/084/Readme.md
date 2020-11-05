
# SELinux Setup & Another Speedrun

## Introduction

Yesterday I setup a new VM not using the Linux Foundation provided vmdk file. I was still using CentOS 7, however by default SELinux is enabled and enforcing, whereas the Linux Foundations VM default settings are set to disabled which made it difficult to meaningfully practice setting context labels on directories and ports.

I also completed labs in the following areas from scratch:
- persistent networking with systemd-networkd
- modifying systemd services
- making systemd-journald persistent
- altering rsyslog configuration
- managing the boot procedure by altering and saving changes to ```/etc/defaults/grub```
- firewalld and iptables
- creating encrypted partitions
- creating logical volumes and then changing their size


## ☁️ Cloud Outcome

I get faster with each speedrun and rely less on man pages or google search. 

## Next Steps

Next labs should include the following:
- redo RAID solutions from scratch
- user quota
- managing ssh services
- managing web services
- virtual hosts
- configuring ftp services
- DNS
- NFS and CIFS
- mariadb
- squid web proxy
- containers

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1324310968218849281)