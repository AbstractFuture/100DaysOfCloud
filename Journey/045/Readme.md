
# Virtual Hosts

## Introduction

After redoing the virtual hosts lab, I found that not only was it more complicated than I remembered, but I couldn't properly recall the order of steps to take to resolve virtual hosts.

## Use Case

A single apache process can handle many different hosts, for example it can handle a hundred host names so only needing a single apache httpd process makes things relatively simple if you have 100 website domain names. 

## Cloud Research

Note that steps roughly described here may be innacurate (after all, I struggled to produce the results I wanted) so do your own research before implementing.

I needed to:
- add the ip address and domain name (along with a shortcut name) to ```/etc/hosts``` file
- alter the httpd configuration file at ```/etc/httpd/conf/httpd.conf``` to check the files for virtual host configuration that I would be making in this exercise
- create the virtual host configuration files in the snap in directory located in ```/etc/httpd/conf.d/```
- make both the directory I specified in ```/etc/httpd/conf/httpd.conf``` as well as the child directory for each virtual host configuration file I created
- create the index.html file in each child directory which corresponds to each virtual host I have added
- change the selinux policy, apply the context label to the directory that I specified in ```/etc/httpd/conf/httpd.conf``` and then reboot
- use ```curl``` to get the contents of our virtual host: ```curl http://[virtualhostnamegoeshere]```
- sigh in relief that it all worked

## Next Steps

I'll be getting more familiar and detailing this process a bit better such that I can a) memorize the correct procedure and b) implement it quickly within a time limit

## Social Proof

[Tweet](https://twitter.com/lrnallday/status/1308593911116464134)
