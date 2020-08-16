# Systemd Service Restarts

## Introduction

If any service on your system is important (I'll go ahead and assume there is at least one) then it is worth ensuring that it restarts in the event that it crashes. This article will focus on how to enable that restart functionality but also demonstrate how to restart multiple services in the event that the failed service needs other services restarted as well.

## Prerequisite

This tutorial will use a CentOS 7 VM and I have not yet tested this on Ubuntu so I cannot vouch that these steps are reproducible across other distros. 

## Try yourself

We will configure the httpd service such that it will also vsftpd service.

We first verify that the services we intent to alter are already installed.

```
[root@centos ~]# rpm -qa | grep httpd
httpd-tools-2.4.6-93.el7.centos.x86_64
httpd-2.4.6-93.el7.centos.x86_64
[root@centos ~]# rpm -qa | grep vsftpd
vsftpd-3.0.2-27.el7.x86_64
```

We've verified that both httpd and vsftpd are installed on the system. 

Since we intend to alrer vsftpd to start when our httpd service starts we should disable for the time being.

```
[root@centos ~]# systemctl disable --now vsftpd
[root@centos ~]# systemctl stop httpd
[root@centos ~]# systemctl edit httpd.service
```
The httpd.service snap-in override.conf file currently looks like this in my system because I've already made the file specify that in the event of a crash, I want it to restart. If you haven't created this file before - not a problem! Simply stop the service like I showed you and then edit the service. By doing so you'll create a new file that you can edit and just paste in the following code into that new override.conf file:
```
[Service]
Restart=on-failure
RestartSec=42s
```
We're also going to add the following lines such that whenever httpd.service is started it will start vsftpd.service. 

Our new override.conf file should now look like this:

```
[Service]
Restart=on-failure
RestartSec=42s

[Unit]
Requires=vsftpd.service
```

Save and exit. We need to restart our http.service now since we stopped it so we could edit the .conf files. 

```
[root@centos ~]# systemctl restart httpd.service
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
  Drop-In: /etc/systemd/system/httpd.service.d
           └─override.conf
   Active: active (running) since Sat 2020-08-15 19:20:02 CDT; 48s ago
     Docs: man:httpd(8)
           man:apachectl(8)
 Main PID: 3613 (httpd)
   Status: "Total requests: 0; Current requests/sec: 0; Current traffic:   0 B/sec"
   CGroup: /system.slice/httpd.service
           ├─3613 /usr/sbin/httpd -DFOREGROUND
           ├─3620 /usr/sbin/httpd -DFOREGROUND
           ├─3621 /usr/sbin/httpd -DFOREGROUND
           ├─3622 /usr/sbin/httpd -DFOREGROUND
           ├─3623 /usr/sbin/httpd -DFOREGROUND
           └─3624 /usr/sbin/httpd -DFOREGROUND

Aug 15 19:20:02 centos systemd[1]: Starting The Apache HTTP Server...
Aug 15 19:20:02 centos httpd[3613]: AH00558: httpd: Could not reliably determine the server's ...sage
Aug 15 19:20:02 centos systemd[1]: Started The Apache HTTP Server.
Hint: Some lines were ellipsized, use -l to show in full.
[root@centos ~]# systemctl status vsftpd.service
● vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Sat 2020-08-15 19:20:02 CDT; 2min 33s ago
  Process: 3614 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=0/SUCCESS)
 Main PID: 3616 (vsftpd)
   CGroup: /system.slice/vsftpd.service
           └─3616 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

Aug 15 19:20:02 centos systemd[1]: Starting Vsftpd ftp daemon...
Aug 15 19:20:02 centos systemd[1]: Started Vsftpd ftp daemon.
```
You'll see I checked the status of both services and in fact they are both up and running. 

## Final Thoughts

If any service is critical to your system - I highly recommend adding in this override conf file so that it can restart itself. Remember that we shouldn't approach a problem with 'will it crash?' but with a mindset of 'given that it will crash at some unknown point in the future, what can we do today to recover from that event?".

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1294798428921376773)
