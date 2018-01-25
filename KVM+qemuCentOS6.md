---
title: KVM+qemuCentOS6
layout: default
---

KVM Centos6
<http://www.howtoforge.com/how-to-install-kvm-and-libvirt-on-centos-6.2-with-bridged-networking>
<http://centos.digitalcompass.net/centos/6.2/os/x86_64/> ---Grub -&gt;
vmlinuz initrd=initrd.img console=ttyS0,115200 text

``` bash
# yum install qemu-kvm
# chkconfig libvirtd on
# groupadd libvirt; usermod -a -G drew
-> fix policykit permissions on /dev/kvm 
# groupadd tun; chown root:tun /dev/net/tun; usermod -a -G tun drew
```

``` bash
# cat /etc/sysconfig/network-scripts/ifcfg-eth0;
DEVICE="eth0"
HWADDR="BC:30:5B:DF:E7:59"
ONBOOT="yes"
BRIDGE=br0
```

``` bash
# cat /etc/sysconfig/network-scripts/ifcfg-br0;
DEVICE="br0"
TYPE=Bridge
DELAY=0
ONBOOT="yes"
BOOTPROTO=static
IPADDR=96.31.87.178
NETMASK=255.255.255.192
```

``` bash
$ virt-install --name drew01 --ram 512 --vcpus=1 --arch=x86_64 --hvm --os-type=linux --nographics --disk path=/home/aholt/drew.img,size=5,sparse=true --cdrom CentOS-6.2-x86_64-netinstall.iso
$ virt-install --name drew01 --ram 512 --vcpus=1 --arch=x86_64 --hvm --os-type=linux --nographics --import --disk path=/home/aholt/drew.img
$ virsh --connect=qemu:///system start drew01
$ virsh autostart drew01
```

``` bash
$ virt-install --name connor01 --ram 512 --vcpus=1 --arch=x86_64 --hvm --os-type=linux --disk path=/home/cpenhale/cpenhale.img,size=5,sparse=true --cdrom pfSense-2.0.1-RELEASE-amd64.iso --hvm --vnc --noautoconsole
```

``` bash
$ virsh -c qemu+ssh://aholt@enc02.destinationradiodenver.com/system sysinfo 
$ virsh -c qemu:///system console drew01
$ virsh -c qemu:///system sysinfo
$ virsh undefine <vm>
$ virsh start <vm>
$ virsh shutdown <vm> # graceful shutdown
$ virsh destroy <vm> # hard shutdown, essentially pulling the power cord
$ virsh suspend <vm>
$ virsh resume <vm>
```

Instead of allowing virt-manager to create a new drive image, simply
direct it to use the image you created in the previous step. 3. Create
the overlay:

``` bash
$ qemu-img create -f qcow2 -b <image name>.qcow2 <image name>.ovl
```
