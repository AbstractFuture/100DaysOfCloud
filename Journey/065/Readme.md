
# LVM Practice & LXC Container Troubleshooting

## Introduction

Today I focused on redoing my old LVM lab tasks from scratch and looking up commands I forgot via man pages.

I also fixed my lxc container errors.

## Prerequisite

A CentOS 7 VM.

## Use Case

LVM allows data be stored across several different partitions which may span several different physical devices. Pretty neat.

## Try yourself (Fixing LXC Errors)

If:

- ```lxc-checkconfig``` yields no obvious errors, and everything is green and enabled
- You can create an lxc container (list existing containers with ```lxc-ls -f```)
- You cannot start lxc-containers because the virtual ethernet bridge cannot be found

Then check the status of libvirtd with;

```
$ systemctl status libvirtd
```

In my case this was disabled. Once I started libvirtd I could successfully start the lxc container. 

On my previous VM I had enabled libvirtd (meaning the service would start automatically) and never needed to stop or disable it which is why I forgot about this service. 

Note to self; don't forget about libvirtd. 

## ☁️ Cloud Outcome

You should be able to start your lxc containers.

## Next Steps

More LVM practice and other storage management tasks all within a timed limit in preparation for the LFCS exam.

## Social Proof

[Tweet]()
