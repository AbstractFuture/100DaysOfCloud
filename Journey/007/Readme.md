# Global Aliases In Ubuntu & CentOs (pt 1)

## Introduction

This blog post was inspired by the difficulty I had of reproducing steps in alias tutorials across different distros.

## Prerequisite

I recommend having a VM for both Ubuntu and CentOS so you can expiriment with your own ideas.

## Use Case

A well known benefit of tech is automation. Why do something in a long arduos manner over and over again if we can take the time to automate it and reduce our workload? 

This line of thinking extends to the lengths of commands we use while navigating in the terminal. If you are always connecting to the same remote machine via ssh then you can make the entire command (the ip address and user name) into a single command as opposed to typing out the ip each time you want to make a connection.

While at the terminal we can check what current aliases we have.

```
$ alias

alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'

$ alias s="ssh user@ipaddrgoeshere"
$ alias

alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
alias s="ssh user@ipaddrgoeshere"
```

Now when we wish to access our remote machine we do not need to retype the full command, we only need to type 's'. 

You'll notice I used a single character as the alias which is not a best practice but it will suffice for the purposes of this demonstration.

Please note that when the alias you're setting up has a space in it, you'll need to convert the entire thing into a string for it to be processed correctly.

Well that answers how we set up and alias. But where do we set it up when we wish to make these into global aliases that will apply to all users?

## Cloud Research - Global Aliases

We can setup aliases on the commandline but these aliases will be reset when you exit the shell. If you want your alias to be global then you will need to edit some files.

In my opinion, configuring global aliases is simpler in CentOS. By default if we want our aliases to be global then we will edit /etc/profile file. 

Altering the CentOS files for global aliases is as follows: login as root and perform the following commands

```
$ nano /etc/profile.d/example.sh
```

In your newly created file enter the following text:
```
alias ipconfig='ip addr show'
```
Save and exit. Then log into another user to see if the changes for our alias have taken place.
```
$ su - student
$ ipconfig

1: lo:  mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s3:  mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:67:36:83 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic enp0s3
       valid_lft 85548sec preferred_lft 85548sec
    inet6 fe80::a456:e613:16ff:b150/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
Success! Our changes were saved and our alias can be used by other users.

## End Of Part 1

In part 2 I'll detail the different steps I took to make it work on Ubuntu.
## Social Proof

[Tweet](link)
