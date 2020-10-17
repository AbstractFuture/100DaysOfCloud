
# LFCS Speed Run (Sample Exam)

## Introduction

Today I completed the LFCS practice exam in under an hour.

## Prerequisite

A CentOS 7 VM and the sample exam provided by the LFCS, which you can find on day66 of my 100DaysOfCloud journey.

## Cloud Research

A good way to look at this is "So you speedran the exam, but did you answer the questions well?". And in retrospect there were 2 basic questions I was incorrect on. Firstly, using tar syntax and secondly, I failed to alter the init sequence such that the rc.local would run at boot time. 

This rc.local task was a bit nuanced (in my opinion) so let me share my process with you all. The task is as follows: Alter the init boot sequence so that the ​ rc.local​ or boot.local​ script (depending on the distribution that you have selected) is executed at boot time.

The steps I took were;

Checking out the file contents of rc.local

```
# vim /etc/rc.d/rc.local
```

The commented notes explained I needed to make this executable such that it could be used at boot time.

```
# chmod +x /etc/rc.d/rc.local
# ll /etc/rc.d/rc.local
```
But what I failed to do was enable the service via systemctl.

```
# systemctl status rc-local
# systemctl enable --now rc-service
```

## Try yourself

Check out the LFCS sample exam and see if you have any difficulty completing the exercises.

## Next Steps

Practice regarding: LVM, RAID, SELinux, and networking.

## Social Proof

[Tweet]()
