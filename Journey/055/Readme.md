
# Proxies: More complicated than I expected

## Introduction

Proxies can restrict what sort of requests will leave the network. My lab involved adding specific domains to the proxy configuration file that would not allow the request to be processed.

## Prerequisite

A CentOS 7 VM.

## Use Case

Proxies allow a sysadmin to prevent users from accessing irrelevant content. 

## Cloud Research

I didn't expect to have such a hard time with this lab. Nearly all of it was trouble shooting. 

It appears there was a syntax error in the instructors notes such that my configuration was not correct, but even after fixing this, I cannot block the test url of ```redhat.com```.

Very strange.

## Try yourself

Go ahead and download ```squid``` if it isn't on your system. For LFCS purposes, you should enable the service right away or you may forget to do so later and lose marks on the service configuration setup. Continue the tutorial once the package is downloaded successfully. 

### Step 1 — Edit configuration file

```
# vim /etc/squid/squid.conf
```
The conf file is pretty small so I recommend having a look at it if you are curious. Add the following lines of text where you feel it is appropriate, easy for you to find, and not confusing.

You'll notice we have to have 2 regular expressions specified so we can block both ```http``` and ```https``` domains. 

Syntax shown below is in fact the correct syntax, although I still cannot figure out why it blocks oracle and not redhat (if you happen to know, please reach out to me!! I'm very curious about this).

```
acl blockedsite url_regex ^http://.*oracle.com/.*$
acl blockedsite url_regex ^https://.*oracle.com/.*$

acl blockedsite url_regex ^http://.*redhat.com/.*$
acl blockedsite url_regex ^https://.*redhat.com/.*$

http_access deny blockedsite
```

### Step 2 — Restart and check service status

```
# systemctl restart squid
# systemctl status squid
```

### Step 3 — Alter your firefox web browser process setting via GUI

Go into firefox settings, look for proxy or network settings, choose manual proxy and enter 127.0.0.1 as well as the port number that was specified in ```/etc/squid/squid.conf``` which by default is 3128.

### Step 4 — Confirm that squid denies access

I'm not sure if restarting firefox is required or not but I did so anyways.

Enter the oracle or redhat url and let me know your results! With this configuration, squid did block access to oracle but not to redhat. 

## ☁️ Cloud Outcome

You've configured a proxy to restrict access to specific domains. 

## Next Steps

Up next I'll manage virtualization!

## Social Proof

[Tweet]()