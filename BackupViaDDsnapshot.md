---
title: BackupViaDDsnapshot
layout: default
---

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
