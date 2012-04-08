---
title: UbuntuRAID0ssd
layout: default
---

Ubuntu RAID0 SSD no root w/o boot partition

During install
--------------

### Jump over to another tty

    # apt-get -y install lvm2

### Make sure partition starts on 2048

    # fdisk -l

    Disk /dev/sda: 32.0 GB, 32017047552 bytes
    132 heads, 63 sectors/track, 7519 cylinders, total 62533296 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x000a5046

       Device Boot      Start         End      Blocks   Id  System
    /dev/sda1            2048    62533295    31265624   8e  Linux LVM

    Disk /dev/sdb: 32.0 GB, 32017047552 bytes
    132 heads, 63 sectors/track, 7519 cylinders, total 62533296 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0xd67db81c

       Device Boot      Start         End      Blocks   Id  System
    /dev/sdb1            2048    62533295    31265624   8e  Linux LVM

### Create PV's with aligned metadata

    # pvcreate --metadatasize 250k /dev/sda1
    # pvcreate --metadatasize 250k /dev/sdb1

### Create VG and LV

    # vgcreate  vgssd /dev/sda1 /dev/sdb1
    # vgdisplay vgssd | grep Total
      Total PE              15266
    # lvcreate -i2 -I128 -n lvssd vgssd --extents 15266

### Create file system

    # mkfs.ext4 -v -O ^has_journal -m 0.1 -E stride=32,stripe-width=64 /dev/vgssd/lvssd
    # tune2fs -c 0 /dev/vgssd/lvssd

Post Install Before Reboot
--------------------------

### Add bits for lvm and nfs on next boot

    # mount -o bind /dev /target/dev
    # mount -o bind /sys /target/sys
    # mount -o bind /proc /target/proc
    # chroot /target
    # sudo apt-get -y install lvm2 nfs-common

### /etc/fstab modifications

    UUID="6239bc41-8816-47b6-b7d5-2be592f8b69b" /               ext4    noatime,discard,errors=remount-ro 0 1

    # Keep excessive writes in /tmp, and I use a remote syslog server
    none        /tmp        tmpfs   size=300M   0 0
    none        /var/log    tmpfs   defaults    0 0

    # Mount network raid array and lets keep apt cache over there via bind mount
    192.168.1.20:/mnt/raid5 /mnt/raid5  nfs defaults    0 0
    /mnt/raid5/drew/drew-desktop/archives/ /var/cache/apt/archives/ nfs bind 0 0

### /etc/rc.local additions

    echo deadline >/sys/block/sdg/queue/scheduler
    echo deadline >/sys/block/sdh/queue/scheduler
    find /sys/devices -name nr_requests -exec sh -c 'echo 4096 > {}' \;

### /etc/sysctl.conf additions for swap

    vm.swappiness to 1

### Update grub2

-   Note may require rebuild of initial ram disk -

<!-- -->

    # mv /boot/initrd.img-3.2.0-20-generic initrd.img-3.2.0-20-generic.old
    # mkinitramfs -o /boot/initrd.img-3.2.0-20-generic
    # update-grub
    # grub-install /dev/sda
    # grub-install /dev/sdb

Reboot from Installer
---------------------

Once in OS lets stop a few things from wearing out the SSD's.

### Move Firefox cache off ssd

-   firefox-&gt; <about:config> -&gt; new string -&gt;
    browser.cache.disk.parent\_directory to /tmp/drewff

Sources
-------

-   <https://sites.google.com/site/lightrush/random-1/checkiftrimonext4isenabledandworking>
-   <http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/newmds-ssdtuning.html>
-   <http://www.ocztechnologyforum.com/forum/showthread.php?82648-software-RAID-LVM-TRIM-support-on-Linuxking>
-   <http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/newmds-ssdtuning.html>
-   <https://wiki.archlinux.org/index.php/Solid_State_Drives#Mount_Flags>

