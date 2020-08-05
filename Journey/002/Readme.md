<!-- This template removes the micro tutorial for a quicker post and removes images for a full template check out the 000-DAY-ARTICLE-LONG-TEMPLATE.MD-->



# Finding The Right Commands In Linux

## Introduction

Linux is a big part of cloud computing so it makes sense to me that we should understand linux and bash scripting.


## Finding Commands With man -k

There will be times when we know what goal we want to accomplish inside the bash terminal but don't know the tool or command that will accomplish this. 

This is where the command

man -k 

comes into play. 

## Cloud Research

- ✍️ Document your trial and errors. Share what you tried to learn and understand about the cloud topic or while completing micro-project.

For example, lets say we wanted to change the host name on our linux machine but don't know the command. Our instinct might be to google it, but in some instances it is quicker to use man -k, or in the event you are taking an exam for a tech cert, using google will be prohibited.

Try the following steps in your linux terminal:

- man -k change hostname

The output fills up our entire terminal with all commands that involve change and hostname! That won't do, it's simply too much to read. Let's alter the command a little bit.

- man -k change hostname | wc -l

The wc -l command counts the number of lines that our previous command printed out. My Ubuntu virtual machine says there are 168 lines, meaning there are 168 commands to search through. 

Let's see if we can narrow it down a bit

- man -k hostname | grep change | wc -l

Using grep I search the output of man -k hostname for all instances where 'change' is mentioned, and then wc -l counts how many instances that is. My output is 0, a clear sign to rethink my approach.

Let's the previous command without grepping for 'change'

- man -k hostname | wc -l

output is 17, a feasible amount to manually search through - now that's what I call progress!

So why is it our original output was 168? Originally I made the search too broad. I used 'change hostname' as opposed to just hostname. 

Now that we've found a feasible amount of lines to read through, I have found the following commands that match my search criteria:

freehostent (3)      - get network hostnames and addresses

gethostname (2)      - get/set hostname

getipnodebyaddr (3)  - get network hostnames and addresses

getipnodebyname (3)  - get network hostnames and addresses

hostname (1)         - show or set the system's host name

hostname (5)         - Local hostname configuration file

hostname (7)         - hostname resolution description

hostnamectl (1)      - Control the system hostname

hosts (5)            - static table lookup for hostnames

libnss_myhostname.so.2 (8) - Provide hostname resolution for the locally conf...

nmtui-hostname (1)   - Text User Interface for controlling NetworkManager

nss-myhostname (8)   - Provide hostname resolution for the locally configured...

sethostname (2)      - get/set hostname

ssh-argv0 (1)        - replaces the old ssh command-name as hostname handling

systemd-hostnamed (8) - Host name bus mechanism

systemd-hostnamed.service (8) - Host name bus mechanism


## Next Steps
Now we can use the man or help pages on whichever option is most likely to have the functionality we're looking for. 

Hope that helps!

## Social Proof

✍️ Show that you shared your process on Twitter or LinkedIn

[Tweet](https://twitter.com/lrnallday/status/1290994682328223744)