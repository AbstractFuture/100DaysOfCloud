# LFCS Exam Review pt10

## Introduction

With my LFCS exam booked for this Friday, I took some time to review old labs and concepts.

## Prerequisite

A CentOS 7 VM.

## Cloud Research

I covered many different topics:

- Systemd: using systemd-networkd and systemd-resolved for networking, altering systemd services to be persistent and restart on failure, used systemd timer to schedule services instead of using /etc/crontab, deleted old NetworkManager /etc/resolv.conf file and replaced with a symbolic link to the systemd file /etc/systemd/resolved.conf 

- Syslog: Scheduled cronjobs using the snap-in directories to write messages to syslog

- Scheduling: used at's intuitive syntax to schedule jobs 5 minutes in the future and then monitor processes related to that job

- hostnamectl: changed hostname using hostnamectl

- ports: checked open ports using netstat -tulpen and ss -tuna

- PAM: revisited how to alter pam files, changed which tty were regarded as secure and altered PAM files such that logging into root in an unsecure tty was not possible

## Try yourself

Review my previous 26 days for more specifics about each of the above topics.

## Next Steps

✍Continuing with LFCS exam reviiew! Containerization, more LVM tasks, and scheduling scripts that kill or enable processes.

## Social Proof

[Tweet]()
