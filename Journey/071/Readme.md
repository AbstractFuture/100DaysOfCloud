
# LFCS: compiling exam questions

## Introduction

Today I compiled a list of questions to speedrun for the lfcs.

## Prerequisite

A CentOS 7 VM.


## Cloud Research

The questions I compiled covered about half of the LFCS content and I completed it within the hour. I consider that a good sign, assuming the remaining 50% of the content takes the same amount of time to complete.

I also changed the setup of the VM to mimic the exam environment a bit better by setting the default boot mode to ```multi-user.target``` as opposed to ```graphical.target```.

You can alter these default settings in CentOS 7 using the following commands;

```
# systemctl get-default
# systemctl set-default multi-user.target
```

Setting the default from graphical to multi-user won't take effect until reboot but you can enter multi-user mode right away using;

```
# systemctl isolate multi-user.target
```

## Social Proof


[Tweet](https://twitter.com/lrnallday/status/1319366378521038848)
