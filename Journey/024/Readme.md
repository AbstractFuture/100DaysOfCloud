# LFCS Exam Review pt7

## Introduction

Focused on networking utilities and concepts. 

## Prerequisite

CentOS 7 or Ubuntu VM

## Cloud Research

The materials I reviewed are 
- ip addr show
- hostnamectl
- ifconfig
- ss -tuna
- nmap
- dig
- ip route show
- ping
- /etc/resolve.conf

## Try yourself

To learn more about your network configuration, use the following commands:

```
$ ip addr show
```
```
$ ip route show
```
```
$ cat /etc/resolv.conf
```
Before moving into more complex troubleshooting it is worthwhile to start with the simple utilities. See if you can ping google.

```
$ ping google.com
```
To learn more about what services are offered by the service, use ```ss``` , the socket status utility.

```
$ ss -tuna
```
Check the man pages for a better understanding of the options ```ss``` can accept.

The ```nmap``` utility is an advanced network analysis tool. If you were to use it on a public network, it will be regarded as a hostile action. DO NOT use it on a public network. You have been warned. 

I do, however, recommend using it to analyze your own private network. 

## Next Steps

I intend to cover LVM (logical volume management) and other partition related things. I'm considering creating a few brief tutorials on the material I've covered thus far as well.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1299746245896998914)
