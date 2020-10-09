
# Docker Made Easy For The LFCS

## Introduction

This will be a summary of commands you ought to know for the lfcs. No fluff.

## Prerequisite

A CentOS 7 VM.

## Try yourself

### Step 1 — Downloading Docker

```
$ yum install docker
```

### Step 2 — Download & run image

```
$ systemctl start docker
$ docker search nginx
$ docker run nginx
```

### Step 3 — Verify Container Status

```
$ docker ps
```
Output should show all running containers

### Step 4 — Change Restart Policy

While you could also run the container for the first time with the restart policy enabled I chose to do it afterwards.

Take the container ID from the output of ```docker ps``` and use it in the following command;

```
$ docker update --restart always <container id goes here>
```
### Step 4 — Test & Verify

```
$ docker stop <container id goes here>
$ systemctl stop docker
$ systemctl start docker
$ docker ps
```
So we have stopped the container, stopped restarted docker and lastly checked the output of ```docker ps``` which shows us running containers.

The output should indicate that it is running! Congrats!

## ☁️ Cloud Outcome

This is all you need to know with regards to docker and the LFCS.

## Next Steps

Next I will cover LXC containers for the LFCS.

## Social Proof

[Tweet]()