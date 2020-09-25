

# Virtual Hosts

## Introduction

Today I redid the virtual host labs, which I breifly detailed in my last blog post, and learned about the SELinux component to virtual hosts or more specifically apache.

## Prerequisite

Check out the previous day's blog post for the steps taken thus far. I'm using a CentOS 7 VM which uses different conventions than ubuntu regarding virtual hosts and security.

## Cloud Research

In order for apache to access the directory we specified in ```/etc/httpd/conf/httpd.conf``` we need to alter the selinux policy, reboot, and then apply the context label to the directory we specified.

Use man pages for these utilities for further reading:
- semanage
- restorecon

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1309315700650119168)
