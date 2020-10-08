
# KVM For LFCS

## Introduction

While I covered the necessary packages to set up a KVM virtual machine on day56, today will cover the commands assuming all packages are installed (like they will be for the LFCS)

## Prerequisite

A CentOS 7 VM with the following packages installed:

- qemu-kvm
- libvirt
- libvurt-client
- virt-install
- virt-viewer
- virt-manager

The following services must be enabled:

- libvirtd

## Cloud Research

The commands are fairly easy and straightforward (at least with regards to the LFCS). They involve listing enabled or all VMs, stopping/starting VMs, and auto starting VMs. 

## Try yourself

### Step 1 — Enable libvirtd

```
# systemctl enable --now libvirtd
```

### Step 2 — View all VMs

To see running VMs use:
```
# virsh list
```

To see all VMs use:
```
# virsh list -all
```

### Step 3 — Start Or Stop A VM

Starting a VM from CLI:
```
# virsh start vmnamegoeshere
```

Stopping a VM from CLI:
```
# virsh destroy vmnamegoeshere
```

Don't be intimidated by the ```destroy``` option. Once you use it you can verify that it stopped the VM and didn't delete it with ```virsh list --all```.

### Step 4 — Autoenabling VMs

To have VMs automatically start use:
```
# virsh autostart vmnamegoeshere
```

## ☁️ Cloud Outcome

You now know all you need to know regarding the LFCS and KVM!

## Next Steps

I intend to do more docker practice, specifically around auto starting containers, and then a timed review of all labs completed thus far.

## Social Proof

[Tweet]()
