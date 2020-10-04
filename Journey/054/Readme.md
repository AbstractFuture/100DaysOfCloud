
# Mail on Linux

## Introduction

The LFCS probably won't cover too many complicated topics related to mail, but you will need to know the basics of email handling, configuring postfix, and configuring dovecot as an imap server.

## Prerequisite

A CentOS 7 VM.


## Cloud Research

I have a grasp of configuring postfix but require more time to configure and memorize the dovecot steps. Therefore this tutorial will focus on postfix.

## Try yourself

We'll be configuring a postfix server to accept messages from other servers.

### Step 1 — Comment out the following lines

Open up the main postfix configuration file ```/etc/postfix/main.cf``` with your choice of text editor and comment out the following lines like so:

```
#inet_interfaces = localhost
```

```
#mydestination = $myhostname, localhost.$mydomain, localhost
```

```
#myorigin = $myhostname
```

### Step 2 — Uncomment the following lines

Uncomment these existing lines like so:

```
inet_interfaces = all
```

```
mydestination = $myhostname, localhost.$myhostname, localhost, $mydomain
```

```
myorigin = $mydomain
```

### Step 3 — Add in the following new lines

Add in the following new lines where the cluster of  ```mynetworks``` paramater settings are.

```
mynetworks = youripandsubnetmaskgohere
```

### Step 4 — Alter this existing setting

Search the following string ```inet_protocols = all``` and replace ```all``` with ```ipv4``` otherwise it will search for ipv6 addresses and if you have not properly configured everything related to ipv6 correctly then you will have some very troublesome errors.

## ☁️ Cloud Outcome

You've now configured the fule such that postfix will accept messages from other servers.

## Next Steps

Configuring a web proxy for the LFCS practice.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1312549912693923840)
