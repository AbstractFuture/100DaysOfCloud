
# Speedrun & Web Servers (Including VirtualHosts)

## Introduction

Today I continued to speedrun old labs, and still need to do better reagrding the SELinux and httpd content, but I am indeed making progress.

## Prerequisite

A CentOS 7 VM.

## Cloud Research

My web server lab included setting up an index in the default document root specified in ```/etc/httpd/conf/httpd.conf``` and then setting up configurations whith directories not in the configuration file.

After settting up both the configuration file, the index file, and the directories, I needed to use SELinux to permit this action (hence how I learned I need more practice with SELinux). 

A minor side note: I'm debating between simply using vim for all my networking configuration since it requires less troubleshooting than NetworkManager and its cli tools, or systemd-networkd. It would definitely be wise for me to do some practice solely using vim to configure networking before going into the LFCS.

## Next Steps

- DNS, FTP, SAMBA, MariaDB, and web proxies
- more speedruns so I can become more efficient

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1322136538491375617)
