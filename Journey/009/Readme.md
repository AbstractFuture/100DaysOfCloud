

# PAM Files

PAM stands for Pluggable Authentication Modules. They are used to set authentication policies, like login for example. 

You can find PAM files with:
```
$ ls /etc/pam*

/etc/pam.conf

/etc/pam.d:
chfn                           cron                    newusers   su
chpasswd                       cups                    other      sudo
chsh                           dovecot                 passwd     systemd-user
common-account                 gdm-autologin           polkit-1   vmtoolsd
common-auth                    gdm-fingerprint         ppp        vsftpd
common-password                gdm-launch-environment  runuser
common-session                 gdm-password            runuser-l
common-session-noninteractive  login                   sshd
```

You can check out these files with any text editor. We can use 'login' for our example. If you've read the rest of my posts thus far you know the conventions Ubuntu and CentOS use differ. We see that yet again in this example.

In Ubuntu, most of the file is commented text explaining what each setting means. While friendly to average or new users, it is a bit disorienting and looks messy. Contrast that to CentOS' neat and minimal login setup file.

While I don't intend to paste both file contents here in this blog post (and besides, shouldn't you be getting more VM practice? If you haven't set up both an Ubuntu VM and a CentOS VM I would encourage you to do so - it will make it easier to follow along), I would like to count the number of lines in each OS to give you an idea of how minimal the CentOS version is.

In Ubuntu:
```
$ cat login | wc -l

116
```

And in CentOS:
```
$ cat login | wc -l

18
```

Quite a difference! But the minimal approach is only useful if you already know what is contained in each file and what the implications are for changing the settings.

Incorrectly configuring PAM files can result in you being unable to login again! This is why I highly recommend to start setting up VMs. It's better to break a toy car than totally demolish a real one.

## Useful Links
[Linux Pluggable Authentication Modules (PAM)](https://www.youtube.com/watch?v=uebQr2KvQzA)

[Using Pluggable Authentication Modules (PAM)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/managing_smart_cards/pluggable_authentication_modules)

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1293713068330033155)
