
# LFCS Exam Review pt19

## Introduction

Continued LFCS exam review. Focused on ssh related commands.

## Prerequisite

I used a CentOS 7 VM but all linux distros should have ssh installed. If not then download it with your package manager of choice.

## Use Case

Allows a user to interact with a remote machine. SSH is also encrypted so passwords or other info are not plaintext and therefore not vulnerable to a man in the middle attack.

## Cloud Research

The configuration of SSH daemon is in the ```/etc/ssh/sshd_config``` file, not to be mistaken with ```/etc/ssh/ssh_config```.

Related ssh commands are as follows:

- ssh-keygen

- ssh-copy-id

- ssh-agent

- ssh-add


## Try yourself

I'm running a CentOS 7 VM on an ubuntu machine, and successfully logged into my ubuntu home computer from the VM. 

If you aren't running linux, you could set up 2 linux VMs and practice that way, or use PuTTy and ssh into a remote linux machine.

## Social Proof

[Tweet]()
