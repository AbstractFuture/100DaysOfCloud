
# Working With Files (& a quick container review)

## Introduction

Today I practiced working with files using the ```find``` command, created hard links, and reviewed the docker and lxc commands I could recall. 

## Prerequisite

A CentOS 7 VM is required.

## Working With Files

I use ```find``` command to locate all files on my system with a size bigger than 100 MiB and write the results of that command to a new file ```/tmp/bigfiles```.

```
$ man find # I needed to consult the man page because I forgot what the default size paramater was
$ find / -size +100M  
```
I confirm that the output looks appropriate but to make it more readable I direct the error messages to ```/dev/null```.

```
$ find / -size +100M 2>/dev/null
```

Perfect - the output is readable and I now direct that output to a new file in my ```/tmp``` directory.

```
$ find / -size +100M 2>/dev/null > /tmp/bigfiles
```

Now that a list of all files on the system is created I need to create a hard link which points to that location.

```
$ ln /tmp/bigfiles /root/bigfiles
```

I got no errors so I confirm that the target file and link name file share the same inode number.

```
$ ls -li /tmp/bigfiles /root/bigfiles
```

Success!

## Container Recap

### Docker Commands

- yum install docker
- systemctl start docker
- docker search
- docker pull
- docker start --restart always nginx # or any container name
- docker ps
- docker stop
- docker restart

### LXC Commands

- yum install epel-release
- yum install lxc lxc-templates lxc-extra
- lxc-checkconfig
- lxc-create 
- lxc-start
- lxc-stop
- lxc-ls -f
- lxc-autostart


## Next Steps

Probably some more practice with adding users, modifying user default settings and some more lab review.

## Social Proof

[Tweet]()