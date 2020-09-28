
# DNS (more complicated than I thought!)

## Introduction

Alright I admit it! Even though the practice labs instructions are straightforward, I don't quite have the hang of it just yet.

## Prerequisite

A CentOS 7 VM.

## Cloud Research

I tried to configure a caching only DNS name server, but I realize my fundamentals aren't strong enough to easily complete this task. 

New concepts included the unbound package and its conf file, learning which ports unbound uses (it was so frustrating to try and comprehend these error messages with ```systemctl status -l unbound``` without understanding what ports the service would occupy), learning how ```named``` which for whatever reason was not installed by default even though its utils were(??) so I couldn't locate it's conf file until I figured that out, as well as all the specific configurations I need to add into the ```unbound.conf``` file which I have yet to memorize or really understand.

Some difficulties included the sheer file size of ```/etc/unbound/unbound.conf``` which is a whopping 862 line file. Locating the settings I need and even recalling which settings to alter is still a challenge.

While I did manage to complete the lab, I can tell I don't understand why/ how it works. But like with most things; practice makes perfect. 

## Try yourself

Heres a [tutorial](https://calomel.org/unbound_dns.html) I found that may walk you through the installation and give much more information than I can.

## ☁️ Cloud Outcome

If done successfully, you should have the ```unbound``` service successfully running. Verify with:

```
# systemctl status -l unbound
```

## Next Steps

Learning about NFS and CFIS file sharing, and perhaps data base configuration as well.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1310410493811666945)
