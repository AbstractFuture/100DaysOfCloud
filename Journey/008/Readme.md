# Global Aliases In Ubuntu & CentOs (pt 2)

## Introduction

This is part 2 of this blog post that I started on day 7. 

As a recap: we've successfully created an alias in CentOS very simply.
You can find that tutorial here: [Part 1](https://github.com/AbstractFuture/100DaysOfCloud/blob/main/Journey/007/Readme.md).

## Prerequisite

This demonstration will be in an Ubuntu VM so I recommend setting up your VM if you haven't already (and besides, it's good practice for you!).

## Try yourself

Like last time we will set up a new file in /etc/profile.d/ which will contain our alias.
```
$ sudo nano /etc/profile.d/student.sh
```
And add in the following alias into your newly created file.
```
alias ipconfig="ip addr show"
```
Save your file, exit the shell, and reboot your VM. 
```
$ ipconfig

Command 'ipconfig' not found, did you mean:

  command 'ifconfig' from deb net-tools
  command 'iwconfig' from deb wireless-tools
  command 'iconfig' from deb ipmiutil

Try: sudo apt install <deb name>
```
So clearly, this is not what we wanted to have happen. 

I add the following code to the /etc/profile.d/student.sh file to determine if my file is being read at all.
```
export COLOR=red
```
This bit of code doesn't do anythign except for create a shell variable. I only want to know if I can perform ```$ echo $COLOR ``` to determine if my student.sh file is being read at all.

After adding in that code, saving, and rebooting, my shell will in fact echo 'red' to stdout but it still doesn't recognize my ipconfig alias. 

After searching for on (mostly) the Ubuntu forums I learned that sometimes files in the /etc/profile.d directory are ignored. I also learned that a global bashrc file existed so I added my alias there. You will need to use root privaleges to edit the bash.bashrc file. 

I'd also like to point out that the reason I didn't edit the .bashrc file in the home directory is because I wanted this alias to be available to all users as opposed to only one.

```
$ sudo nano /etc/bash.bashrc
```
Add in the alias to the bottom of the file:
```
#lfcs practice
alias ipconfig="ip addr show"
```
Save, exit and reboot vm. Afterwords I try the ipconfig alias in terminal and it works! 
```
$ ipconfig
1: lo:  mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: enp0s3:  mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:62:b4:7e brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86367sec preferred_lft 86367sec
```
I want to point out that I'm not sure why the output between Ubuntu and CentOS is different, but that is a subject of research for another day.

## Helpful Links
[Aliases in subshell / child process](https://superuser.com/questions/319538/aliases-in-subshell-child-process)

[How Can I Preset Aliases For All Users](https://askubuntu.com/questions/610052/how-can-i-preset-aliases-for-all-users)

[Scripts in /etc/profile.d Being Ignored?](https://askubuntu.com/questions/438150/scripts-in-etc-profile-d-being-ignored)

[Understanding .bashrc and .bash_profile](https://askubuntu.com/questions/121413/understanding-bashrc-and-bash-profile)


## Social Proof

[Tweet](link)
