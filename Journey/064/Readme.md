
# Advanced Linux Permissions (& More VM troubleshooting)

## Introduction

While the basic permissions yesterday focused on file and group ownership as well as chmod values, todays lab dealt with ```SGID``` and ```stickybit```.

I also am experiencing an LXC issue I had not encountered previously. While ```lxc-checkconfig``` shows a green status of all settings enabled, I am unable to start the container because the virtual ethernet bridge is throwing an error. I need to investigate further.

## Prerequisite

A CentOS 7 VM and a working LXC configuration.

## Cloud Research

### Special Permissions

```SGID``` stands for 'Set Group ID'. It will allow all new files and directories within a directory to automatically be owned by the group owner.

```Stickybit``` allows only the file or directory owner to delete files they have created.

## Next Steps

Next steps include repeating the lab in a much faster time frame and troubleshooting the LXC issues. 

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1316178731480870912)
