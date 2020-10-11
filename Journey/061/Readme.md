
# LXC Container Practice

## Introduction

More container labs! Unfortunately I experienced some errors regarding autostart that I didn't have with docker (check out day60 for that) which I am still trouble shooting.

## Prerequisite

A CentOS 7 VM. 

Also, download the following packages.

- epel-release
- lxc
- lxc-templates
- lxc-extra

## Try yourself

List current running containers:
```
$ lxc-ls -f
```

None should be running. Let's confirm that the downloaded packages are functioning as intended:

```
$ lxc-checkconfig
```
The output (if it is functioning) should be a list of settings set to 'enabled'.

Now let's use the templates we downloaded earlier to create a CentOS lxc container

```
$ lxc-create -t centos -n <containernamegoeshere>
```
The -t option specifies that we are using a script from the template directory at ```/usr/share/lxc/templates/```` and the -n lets us specify the new container name.

```
$ lxc-ls -f
```
You should now see the running container listed. 

Here are a list of other commands you can check the man pages for additional information:

- lxc-info
- lxc-autostart
- lxc-start
- lxc-attach
- lxc-stop

## ☁️ Cloud Outcome

You've got a centos LXC container up and running!

## Next Steps

I'll continue to troubleshoot the autostart erros I experienced. After that I will be doing lab review.

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1315115158528815104)
