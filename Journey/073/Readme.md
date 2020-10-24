
# Scripting, PAM Configs & Networking labs review

## Introduction

Today I reviewed labs with regards to bash shell scripting, changing pam configurations such that certain teletypes were regarded as insecure and root was unable to login, disabling the NetworkManager on CentOS 7 and setting up persistent networking with systemd-networkd and systemd-resolved.

## Prerequisite

A CentOS 7 VM.

## Try yourself

See if you can complete the following tasks

### Bash Shell Scripting

Create and run a script that will print out the name of the user who executed the script as well as print out your default gateway.

### PAM Configuration

Find the file that specifies which teletypes are secure, alter it such that tty4 is now insecure, and alter the appropriate PAM configuration(s) such that root will be unable to login to tty4. 

### Networking With Systemd

Disable NetworkManager and use systemd-networkd to manage networking.

## Next Steps

Do lab review speedrun for all previous labs and then move onto kernel management, boot procedure, firewall, SELinux, LVM, and filesystem/ mounts labs.

## Social Proof

[Tweet]()
