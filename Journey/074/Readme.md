
# systemd-networkd on CentOS 7

## Introduction

Today I focused on memorizing the process for setting up systemd-networkd persistently on CentOS 7.

## Prerequisite

A CentOS 7 VM.

## Use Case

I'm unsure as to whether systemd-networkd will be available by default on the LFCS or if I will be required to set it up. I'll be focusing on DHCP for now but within the week I hope to commit to memory the steps for setting up a static connection as well. 

## Cloud Research

You can use nmtui or nmcli to manage the default NetworkManager but neither of those tools apply to systemd. 

Anyways, lets get into the lab/ walkthrough.

## Try yourself

You'll need to install the following packages before proceeding;

```
# yum install -y systemd-networkd systemd-resolved
```

### Step 1 — Which service is your system running

Confirm which service your system is currently using for networking.

```
# systemctl status systemd-networkd
# systemctl status systemd-resolved
# systemctl status NetworkManager
# cat /etc/resolv.conf
```

NetworkManager is up and running on my system and based on the output of /etc/resolve.conf I can see that it is a file managed by NetworkManager. We will change that in the following steps. 

### Step 2 — Disabling NetworkManager

```
# systemctl disable --now NetworkManager
# rm -f /etc/resolv.conf
```

### Step 3 — Create new directory and links

We need to create a directory that can hold our dhcp configuration and create a symbolic link to systemd-resolved resolv.conf file, which at the present time doesn't exist on our system - don't be concerned about that. Once we start systemd-resolved that will be created. 

```
# mkdir /etc/systemd/network
# ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

### Step 4 — Create the DHCP network configuration file

```
# vim /etc/systemd/network/20-dhcp.network
```
File contents should look like so:

```
[Match]
Name=enp0s3

[Network]
DHCP=yes
```

Verify the name of your network on your VM. In my case it is enp0s3. It may be different for you.

### Step 5 — Enabling systemd-networkd and systemd-resolved

We can now enable and start systemd networking. 

```
# systemctl enable --now systemd-networkd
# systemctl status systemd-networkd
# systemctl enable --now systemd-resolved
# systemctl status systemd-resolved
```

If there are no errors, you have made systemd-networkd persistent on your VM.

### Step 6 — Testing network functionality

```
# ping google.com
```
If you can successfully ping google, you did everything right! 

## ☁️ Cloud Outcome

Congrats! You've made systemd-networkd persistent on your CentOS 7 VM.

## Next Steps

Do lab review speedrun for all previous labs and then move onto kernel management, boot procedure, firewall, SELinux, LVM, and filesystem/ mounts labs.

Also do a speedrun of all previous labs to ensure I have not forgotten anything!

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1320325428704411648)
