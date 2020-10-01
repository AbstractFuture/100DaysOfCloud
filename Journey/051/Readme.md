
# NFS & CIFS/SAMBA

## Introduction

Learned about the commands/procedure to make directories available remotely, and how to manually and persistently mount said directories on remote machines. 

## Prerequisite

A CentOS 7 or Ubuntu VM should suffice.

## Use Case

NFS and CIFS are file sharing protocols. 

## Cloud Research

While the samba procedure is easier to recollect, I find the nature of the lab a bit difficult.

For instance, I am to make directories available using both the NFS and CIFS protocol, and then mount them persistently on another server but the instructor has not demonstrated how to create several servers on a single CentOS 7 VM, and how one of those servers can be an ubuntu machine. 

Therefore while I can make directories available using NFS and CIFS, I am currently unable to mount those directories persistently anywhere.

## Try yourself

To use CIFS/ samba, you'll need to install ```samba``` and to mount it peristently (not covered in this blog post) download ```samba-client``` and ```cifs-utils```. 

```
# yum install cifs-utils samba samba-client
```

Check if the samba installation was successful by verifying that the configuration file exists.

```
# vim /etc/samba/smb.conf
```

For demonstration purposes, this will be a very minimal setup. Add the following code snippet to the end of the file. In this case I am creating a config to use a directory ```/samba``` that I have not made yet.

Note that the valid users need to be an existing linux user. So if you don't have a user named linda, then change it to a user that exists on your system.

```
[samba]
    path = /samba
    writeable = yes
    valid users = linda
```

Write and quit. 

Now make the directory you specified in your samba conf.

```
# mkdir /samba
```

Enable the smb service and confirm the status.

```
# systemctl start smb
# systemctl status smb
```
Confirm that samba is visible to your firewall by checking the output of:

```
# firewall-cmd --get-services
```
Configure your firewall to add samba to run time and then make it persistent.

```
# firewall-cmd --add-service samba
# firewall-cmd --add-service samba --permanent
```

## ☁️ Cloud Outcome

You've now made a directory available for remote machines to access.

## Next Steps

Creating a directory to share via NFS and figuring out how to have several different servers which use different OS on a single CentOS 7 VM such that I can persistently mount these drives on the second server.

## Social Proof

[tweet]()
