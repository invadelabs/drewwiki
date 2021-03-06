---
title: BackupViaDDsnapshot
layout: default
---

Speedup USB HD
--------------

Apped to /etc/sysctl.conf per;

-   <http://www.linux-usb.org/FAQ.html#i5>
-   <http://marc-abramowitz.com/archives/2007/02/17/getting-good-performance-out-of-usb-hard-drives-in-linux/>

``` bash
# Speed up writes on USB HD
echo 1024 > /sys/block/sdf/device/max_sectors;
```

Check Bus Speed USB Peripherals
-------------------------------

``` bash
[root@drewserv devices]# grep "" /sys/bus/usb/devices/*/speed
/sys/bus/usb/devices/1-1/speed:480
/sys/bus/usb/devices/3-2/speed:1.5
/sys/bus/usb/devices/usb1/speed:480
/sys/bus/usb/devices/usb2/speed:12
/sys/bus/usb/devices/usb3/speed:12
/sys/bus/usb/devices/usb4/speed:12
/sys/bus/usb/devices/usb5/speed:12
```

Creating / copying snapshot
---------------------------

``` bash
[drew@drewserv ~]$ sudo lvcreate -L10G -s -n tmpbkup /dev/vg-raid5/lv-raid5 
  Logical volume "tmpbkup" created

[drew@drewserv ~]$ sudo lvs
  LV        VG          Attr   LSize   Origin   Snap%  Move Log Copy%  Convert
  lv-backup vg-backup   -wi-ao 698.63g
  lv-raid5  vg-raid5    owi-ao 698.63g
  tmpbkup   vg-raid5    swi-ao  10.00g lv-raid5   0.13
  lv_home   vg_drewserv -wi-ao 178.44g
  lv_root   vg_drewserv -wi-ao  50.00g
  lv_swap   vg_drewserv -wi-ao   3.94g

[root@drewserv ~]#  date; dcfldd if=/dev/vg-raid5/tmpbkup of=/dev/vg-backup/lv-backup bs=4M; date
Sun Jul 24 05:29:04 MDT 2011
178688 blocks (714752Mb) written.
178850+0 records in
178850+0 records out
Sun Jul 24 12:14:20 MDT 2011

[root@drewserv ~]# tune2fs -U random /dev/vg-backup/lv-backup
tune2fs 1.41.14 (22-Dec-2010)

[root@drewserv etc]# mount /dev/vg-backup/lv-backup /mnt/backup

[root@drewserv backup]# ls -al /mnt/backup
total 33839996
drwxr-xr-x. 12 root root        4096 Jul 24 05:01 .
drwxr-xr-x.  5 root root        4096 Jul 23 19:05 ..
drwxr-xr-x.  5 user user        4096 Jul 24 00:06 backup

[root@drewserv ~]# lvremove /dev/vg-raid5/tmpbkup 
Do you really want to remove active logical volume tmpbkup? [y/n]: y
  Logical volume "tmpbkup" successfully removed

[drew@drewserv ~]$ sudo lvs
  LV        VG          Attr   LSize   Origin Snap%  Move Log Copy%  Convert
  lv-backup vg-backup   -wi-ao 698.63g                                      
  lv-raid5  vg-raid5    -wi-ao 698.63g                                      
  lv_home   vg_drewserv -wi-ao 178.44g                                      
  lv_root   vg_drewserv -wi-ao  50.00g                                      
  lv_swap   vg_drewserv -wi-ao   3.94g                                      
```

USB Hard Drive Perf Tests
-------------------------

``` bash
[root@drewserv backup]# dd if=dell-desktop7.22.2010.tar.gz of=/dev/null bs=4M
6321+1 records in
6321+1 records out
26512197033 bytes (27 GB) copied, 677.563 s, 39.1 MB/s
[root@drewserv backup]# cd

[root@drewserv backup]# dd if=/dev/zero of=/mnt/backup/10Gtest bs=4M count=2500
2500+0 records in
2500+0 records out
10485760000 bytes (10 GB) copied, 316.476 s, 33.1 MB/s

[root@drewserv ~]# umount /mnt/backup/
[root@drewserv ~]# dd if=/dev/vg-backup/lv-backup of=/dev/null bs=4M count=2500
2500+0 records in
2500+0 records out
10485760000 bytes (10 GB) copied, 264.512 s, 39.6 MB/s
```
