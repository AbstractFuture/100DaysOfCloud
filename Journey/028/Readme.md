# LFCS Exam Review pt11

## Introduction

Today I focused on changing default grub settings, troubleshooting with emergency and rescue mode, changing /proc defaults in run-time and persistently, and some firewalld syntax and commands.

## Prerequisite

A CentOS 7 VM. 

## Default Grub Settings

To view your current default settings use:
```
# cat /etc/default/grub
```
Note that changes to this file will not automatically update your ```grub.cfg``` file in ```/boot/grub2/grub.cfg```. You can use ```cat``` on both these files to see a big difference in the way they're written - even without making alterations to ```/etc/default/grub```.

After saving your altered changes, use:

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
```
You can then reboot and verify that your changes have taken place (such as removing the redhat graphical boot mode in quiet).

## Kernel & /proc

Before making changes persistent, you may want to apply said changes in run-time first to verify the kernel behaviour is as you intended. In this example we will be looking at the net related things like ipv4 and ipv6. If you want an idea of what exactly is at your disposal simply use ```ls /proc/```. 

If you want to disable ipv6 on your machine (after verifying that your machine is in fact using ipv6) head on over to ```/proc/sys/net/ipv6/conf/all/``` and list the contents of the directory (although I do recommend checking out each directory on your own so you have a sense of how things are organized). Then perform the following command:

```
# cat disable_ipv6
0
```
While many of these files act like booleans (0 for false or off, and 1 for true or on/enable feature) not all files are configured for a 0 or 1 answer. You can use ```sysctl -a | less``` for the status list of these kernel related things and the number they are set to. 

In the case of ```disable_ipv6``` a 0 or 1 will suffice. Simply overwrite the file contents with a 1 to enable the ```disable_ipv6``` feature. Use:

```
# echo 1 > disable_ipv6
```
Confirm you no longer have an ipv6 address with your favourite command:
```
# ip a
```
or
```
ip addr
```
After verifying that your changes have taken place it is important to keep in mind that we only altered this in run-time and it is not configured persistently, meaning when we reboot these changes will be lost.

To make this persistent, I recommend copying the relevant output from:
```
# sysctl -a | grep disable_ipv6 | head -1
net.ipv6.conf.all.disable_ipv6 = 1
```
You'll notice the output is nearly identical to the path to file only this uses ```.``` as opposed to ```/```. This is important because our persistent conf file that we are about to edit will read the ```.``` and not ```/``` so it's nice to have this format already prepared for us. 

Copy the output and with your favourite text editor open up ```/etc/sysctl.conf``` and add in the following line:
```
net.ipv6.conf.all.disable_ipv6 = 1
```
While this is not an elegant persistent solution it is a functional one. Reboot to verify that the changes are persistent.

## Emergency & Rescue Mode

In the CentOS 7 grub menu you can press 'e' for edit. This will take you to a run-time of the /etc/default/grub setup. 

On the line that indicates it is loading up linux, you can add either of the following lines to enter emergency or rescue mode such that you can trouble shoot and fix your system.

Emergency mode code snippet:
```
systemd.unit=emergency.target
```

Resuce mode code snippet:
```
systemd.unit=rescue.target
```
Both of these troubleshooting methods require you to authenticate as root user. In the even that you do not know the root password, you will be unable to use these two options because you will be unable to authenticate as root. 

We can use the following code snippet instead of emergency or rescue which does not require root authentication, and once we can access the system we can reset root password
```
rd.break
```
I should note that the ```passwd``` command is hard coded to interact with ```/etc/shadow``` and in this rd.break mode it is my understanding that you will (probably) not be interacting with ```/``` which presents a problem: how can we configure our system such that passwd will interact on whatever lvm we are on?

Use ```mount```, find the filesystem that doesn't seem like an init.ramfs file system and remount it with read and write permissions (current permissions will be displayed with ```mount``` so it will be easy to tell if it is read only or read and write). The command will look something like this:

```
# mount -o remount,rw /filesystemgoesherelol/
```
Now that we've enabled read write permissions and remounted we need to tell linux to consider /filesystemgoesherelol/ as root so that passwd can access ```/etc/shadow``` by way of ```/filesystemgoesherelol/etc/shadow```

```
# chroot /filesystemgoesherelol/
```
Upon changing what is regarded as root, you will see your prompt change to something like:
```
sh-2: $ 
```
Which indicates we have changed this successfuly. Then simply enter passwd and change the password and use poweroff and not reboot to ensure changes are implemented.

You've just set a new root password without knowing the old root password!

## firewalld

I'm still practicing with firewalld so I just briefly reviewed some commands:

```
# firewall-cmd --list-all
```

```
# firewall-cmd --get-services
```

```
# firewall-cmd --reload
```

```
# firewall-cmd --add-service=servicenamegoeshere
```

## Next Steps

Continue with exam review: firewalld, containers, lvm, and controlling processes. 

## Social Proof

[Tweet]()
