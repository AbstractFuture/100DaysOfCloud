# Creating Daily Logs

## Introduction

A log is a history of actions or processes that are saved to a file and updated as often or infrequently as you like. You also have the ability to set how long a log file is saved for. You can choose what sort of actions or processes are to be logged as well. 

## Prerequisite

If you've been following the previous posts in the #100DaysOfCloud repo then it should be no surprise that we're continuing this mini tutorial with a CentOS 7 VM. 

## Use Case

One use case for logs is to record all instances where a user logged in remotely. This can be used for threat detection. 

## Try yourself

Before explaining what directories and files are involved I will give a brief overview of snap-in files and the role they play. Consider the following: imagine your whole OS exists in a single script. Making a change to this monolith is very risky and can result in fatal errors. We can solve this by having a main script which will have most of the functionality and then have that main script search for other smaller scripts when needing additional functionality or information. This way we can leave our main script untouched (and therefore not likely to have fatal errors) and we have small scripts that are seperate and easy to trouble shoot/ unit test. 

This is tghe approach behind snap-in files. We have a main script (rsyslog.conf) that can search for additional settings or functionality in other smaller non critical scripts. 

Some things to keep in mind before moving forward: log settings are saved (in CentOs 7) in /etc/rsyslog.conf while snap-in files are in the /etc/rsyslog.d/ directory.

In this example I will demonstrate how to change settings in rsyslog.conf to log all info messages in the system and create new log files daily, as well as retain log files for seven days. Let's get into it.

## Changing rsyslog.conf

I will first confirm that rsyslog.conf is in fact in the /etc/ directory:

```
[root@centos ~]# ls /etc/rsyslog*
/etc/rsyslog.conf

/etc/rsyslog.d:
listen.conf
```
After confirming that both the rsyslog.conf file exists as well as our snap-in directory I edit the conf file and add the following line of code to the RULES section.

```
*.=info                     /var/log/info
```

This bit of code says save all messages that are regarded as information (as opposed to other classifications like warning) and save it to the /var/log/info directory.

Save and exit the rsyslog.conf file.

## Managing Log Rotation

Managing log rotation means how often should a log be used before it is replaced and how long should these old log files be saved for.

Dealing with log rotation means editing the /etc/logrotate.conf file which has a snap-in directory titled /etc/logrotate.d/ 

```
nano /etc/logrotate.conf
```
We'll copy the syntax of an existing logrotate configuration which I will list here for your reference:

```
/var/log/btmp {
        missingok
        monthly
        create 0600 root utmp
        rotate 1
}
```
And we'll copy, paste, append and alter this new snippet of code like so:

```
#lfcs practice
/var/log/info {
    daily
    rotate 7
}
```
Our added code says to create a new log daily and save logs (rotate) for 7 days. We could also have added in this code as a seperate file in the snap-in directory /etc/logrotate.d

## ☁️ Cloud Outcome

You can now create a criteria to log actions and processes as well as configure the log rotation.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1295057087471521794)
