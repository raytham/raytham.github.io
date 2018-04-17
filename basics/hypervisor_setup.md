# Hypervisor Setup

## Delta RPMs
Now that I have a fresh install, I want to grab the latest packages. Before I do this, I wanted to enable delta RPMs.

```
# yum install -y deltarpm
# yum update
```

## Install KVM

### Verify KVM Kernel Modules
```
$ lsmod | grep kvm
```

### Install packages
```
sudo yum groupinstall 'Virtualization Host'
```

## Networking

# Create a Bridge

Create ifcfg-br0
ifcfg-em0 was already created at install. Those same settings get copied over
to ifcfg-br0.
The remaining settings in ifcfg-em0 get removed. The most important part:
it can't have an ip address anymore (gets moved to br0). And you need a BRIDGE=
line.

## References
* [KVM_Virtualization_in_RHEL_7_Made_Easy](https://linux.dell.com/files/whitepapers/KVM_Virtualization_in_RHEL_7_Made_Easy.pdf)
* [What is kernel ip forwarding?](https://unix.stackexchange.com/a/14058)
* [Networking Guide - Red Hat Customer Portal](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/)
