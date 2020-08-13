
# systemd-networkd on CentOS 7 Linux

## Introduction

I was studying up on configuring networks for the LFCS exam when I saw a discrepancy between my tutorial and the LF provided CentOS vm. 

The command I was trying to run after I disabled NetworkManager was:

```
$ systemctl enable systemd-networkd
```

However no file in my CentOS vm was found. I used tab autocomplete to see what was available for my systemd options.

```
systemd-backlight@  systemd-hibernate-resume@   systemd-rfkill@
systemd-bootchart.service   systemd-nspawn@
systemd-fsck@   systemd-nspawn@.service
```
I used ```yum``` to install systemd-networkd successfully but in an LFCS exam you are not allowed to look up things on google. I'm glad I tested this out before hand otherwise I would have been in serious trouble. 

## Downloading systemd-networkd

After re-enabling NetworkManager use the following commands:
```
$ yum -y install systemd-networkd

$ systemctl disable NetworkManager
Removed symlink /etc/systemd/system/network-online.target.wants/NetworkManager-wait-online.service.
Removed symlink /etc/systemd/system/multi-user.target.wants/NetworkManager.service.
Removed symlink /etc/systemd/system/dbus-org.freedesktop.nm-dispatcher.service.

$ systemctl enable systemd-networkd
Created symlink from /etc/systemd/system/multi-user.target.wants/systemd-networkd.service to /usr/lib/systemd/system/systemd-networkd.service.
Created symlink from /etc/systemd/system/sockets.target.wants/systemd-networkd.socket to /usr/lib/systemd/system/systemd-networkd.socket.
```


## Social Proof

[Tweet]()
