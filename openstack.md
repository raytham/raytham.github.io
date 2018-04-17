---
title: OpenStack on KVM
---
# OpenStack on KVM
server 0.us.pool.ntp.org
server 1.us.pool.ntp.org
server 2.us.pool.ntp.org
server 3.us.pool.ntp.org
ftp://mirrors.sonic.net/centos/7/os/x86_64

## Networking

Disable NetworkManager.
```
# systemctl disable NetworkManager  
```

# Packstack




## Controller VM

```
sudo virt-install \
  --network bridge=br0 \
  --name os-controller \
  --memory 8192 \
  --vcpus 2 \
  --disk size=100 \
  --os-variant rhel7 \
  --graphics none \
  --location "ftp://mirrors.sonic.net/centos/7/os/x86_64" \
  --extra-args="console=tty0 console=ttyS0,115200"
```
```
sudo virt-install \
  --name os-controller \
  --memory 8192 \
  --vcpus 2 \
  --disk size=100 \
  --os-type linux \
  --os-variant centos7.0 \
  --network network=default \
  --graphics vnc,listen=0.0.0.0 \
  --noautoconsole \
  --location "/tmp/CentOS-7-x86_64-NetInstall-1708.iso"
```
## References
* <http://www.tuxfixer.com/install-openstack-on-kvm-how-to-configure-kvm-for-openstack/>
* <http://jensd.be/289/linux/start-with-a-simple-2-node-openstack-setup-with-kvm>
* [Configure DevStack with KVM-based Nested Virtualization](https://docs.openstack.org/devstack/latest/guides/devstack-with-nested-kvm.html)
<http://www.dasblinkenlichten.com/building-an-openstack-home-lab-the-lab/>
* <https://serverfault.com/questions/567716/virt-install-ignoring-vnc-port-listen>
