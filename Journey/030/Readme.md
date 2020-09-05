
# LFCS Exam Review pt13

## Introduction

Reviewed containerization with Docker and LXC (Linux Containers).

## Prerequisite

I used a CentOS 7 VM but any distro should suffice.

## Cloud Research

First impressions: I found docker more user friendly than I did LXC. 

Neat tricks: using nmap to scan the docker ip addresses (which all live in the range of 172.17.x.x) such that I can learn which docker container is on which IP address.

Also if I understood correctly, to mount storage to a docker container on your home lab you need to alter the selinux enforcing status to permissive:

```
$ setenforce 0
```
More to come over the next week regarding containers.

## Next Steps

I'd like to learn how to make a docker container run automatically when docker restarts/ starts on next reboot. 

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1302393717303672832)
