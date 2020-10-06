
# More Virtual Machine Prep

## Introduction

Today I installed virtualization software and changed my virtualbox vm settings such that embedded virtualization was possible.

## Prerequisite

A CentOS7 7 VM

## Use Case

Embedded virtualization just means running a VM within a VM. You may find this useful for practicing network connectivity between machines or for kubernetes experimentation. 

## Cloud Research

You need the following packages installed to run a VM from within a CentOS 7 VM:

- qemu-kvm
- libvirt
- libvurt-client
- virt-install
- virt-viewer
- virt-manager

You also need to allocate at least one more CPU to your VM from the virtualbox console prior to starting up your VM, as well as specifically check the setting to enable nested VMs. 

## ☁️ Cloud Outcome

You now have the correct settings and software installed to allow for embedded virtualization.

## Social Proof

[Tweet]()
