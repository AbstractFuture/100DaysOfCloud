
# Lab Review & Getting Locked Out Of My Own System (Thank you based SELinux)

## Introduction

Today I focused on completing all labs within 2 hours. The good news: I'm faster than I used to be. The bad news: I didn't finish within 2 hours.

Also, I dealt with SELinux issues on my VM.

## Prerequisite

A CentOS 7 vm. 

## Cloud Research

While completing the selinux context label task, I learned that selinux was actually disabled. I found that odd because a) selinux is a part of the centos LFCS exam, and b) this vm image was provided by the Linux Foundation for the express purpose of having an environment to practice on.

After enabling SELinux and setting it to enforcing mode I was completely locked out of the system. I couldn't even enter ```rd.break``` in order to reset root password or access the selinux configuration file.I had to destroy the VM and start over from scratch. 

My temporary work around is to set SELinux to permissive mode so that I can assign context labels to files but since SELinux won't be enforcing anything I don't think I can verify if any of my steps would be successful.

Therefore this workaround only allows me to practice entering memorized commands, which may score me some minor points on the LFCS but I definitely won't be able to verify if my solution works which means it is more likely that I will not complete the SELinux tasks in their entirety.

## Next Steps

I'd like to continue the labs regarding lvm, RAID, creating systemd mounts, user quota, managing ssh services, web services, ftp services, and then afterwards go back and reinforce my knowledge about static ip configuration, network configuration using NetworkManager (and nmtui /nmcli), SELinux context labels, and iptables (which I still struggle with.).

## Social Proof

[Tweet]()