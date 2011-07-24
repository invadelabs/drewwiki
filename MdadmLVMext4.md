---
title: MdadmLVMext4
layout: default
---

Preliminaries
-------------

For faster rebuild

    # cat dev.raid.speed_limit_min=100000 # set higher raid rebuild limit >> /etc/sysctl.conf

For Faster Writes Add this to a script on boot ( rc.local )

    # echo 16384 > /sys/block/md127/md/stripe_cache_size

`   ^----- **Beware of RAM usage: Value in pages per device, i.e. on 4 devices at 8192 comes out to 128MB`

Build the array
---------------

    # mdadm -v --create /dev/md127 -l 5 -c 512 --bitmap=internal --raid-devices=3 /dev/sdb /dev/sdd /dev/sde
    -------------------------------------------------------------------------------------------
    [root@drewserv ~]# mdadm -D /dev/md127
    /dev/md127:
            Version : 1.2
      Creation Time : Fri Jul 22 22:24:38 2011
         Raid Level : raid5
         Array Size : 976770048 (931.52 GiB 1000.21 GB)
      Used Dev Size : 488385024 (465.76 GiB 500.11 GB)
       Raid Devices : 3
      Total Devices : 3
        Persistence : Superblock is persistent

      Intent Bitmap : Internal

        Update Time : Sat Jul 23 00:25:31 2011
              State : active
     Active Devices : 3
    Working Devices : 3
     Failed Devices : 0
      Spare Devices : 0

             Layout : left-symmetric
         Chunk Size : 512K

               Name : 127
               UUID : e9355597:7a4ff30b:21b71007:42443f63
             Events : 21

        Number   Major   Minor   RaidDevice State
           0       8       16        0      active sync   /dev/sdb
           1       8       48        1      active sync   /dev/sdd
           3       8       64        2      active sync   /dev/sde

### MD RAID5 Perf Tests

\[root@drewserv ~\]\# dd if=/dev/md127 of=/dev/null count=10000 bs=1M
10000+0 records in 10000+0 records out 10485760000 bytes (10 GB) copied,
63.5414 s, 165 MB/s

Write Test \[root@drewserv ~\]\# cat
/sys/block/md127/md/stripe\_cache\_size 256 \[root@drewserv ~\]\# echo
16384 &gt; /sys/block/md127/md/stripe\_cache\_size \[root@drewserv ~\]\#
cat /sys/block/md127/md/stripe\_cache\_size 16384 \[root@drewserv ~\]\#
dd if=/dev/zero of=/dev/md127 count=10000 bs=1M 10000+0 records in
10000+0 records out 10485760000 bytes (10 GB) copied, 74.9109 s, 140
MB/s

Create LVM VG/PV/LV
-------------------

    [root@drewserv ~]# vgcreate vg-raid5 /dev/md127
      No physical volume label read from /dev/md127
      Physical volume "/dev/md127" successfully created
      Volume group "vg-raid5" successfully created
    [root@drewserv ~]# vgdisplay -v vg-raid5
        Using volume group(s) on command line
        Finding volume group "vg-raid5"
      --- Volume group ---
      VG Name               vg-raid5
      System ID             
      Format                lvm2
      Metadata Areas        1
      Metadata Sequence No  1
      VG Access             read/write
      VG Status             resizable
      MAX LV                0
      Cur LV                0
      Open LV               0
      Max PV                0
      Cur PV                1
      Act PV                1
      VG Size               931.52 GiB
      PE Size               4.00 MiB
      Total PE              238469
      Alloc PE / Size       0 / 0   
      Free  PE / Size       238469 / 931.52 GiB
      VG UUID               MbPYwg-Q12h-YoEq-oh1p-dlKH-HwaP-fiKRzq
       
      --- Physical volumes ---
      PV Name               /dev/md127     
      PV UUID               eeErmO-wm0Z-p870-6uJp-TcMJ-tgSm-NAq1BX
      PV Status             allocatable
      Total PE / Free PE    238469 / 238469
       

    root@drewserv ~]# lvcreate -l 178850 -n lv-raid5 vg-raid5
      Logical volume "lv-raid5" created

    root@drewserv ~]# lvdisplay /dev/vg-raid5/lv-raid5 
      --- Logical volume ---
      LV Name                /dev/vg-raid5/lv-raid5
      VG Name                vg-raid5
      LV UUID                QYuPPT-TqzR-bDC5-6Cjd-DYDj-W102-0oK4Or
      LV Write Access        read/write
      LV Status              available
      # open                 0
      LV Size                698.63 GiB
      Current LE             178850
      Segments               1
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     4096
      Block device           253:4

### LVM Performance Tests

\[root@drewserv ~\]\# dd if=/dev/vg-raid5/lv-raid5 of=/dev/null
count=10000 bs=1M 10000+0 records in 10000+0 records out 10485760000
bytes (10 GB) copied, 67.0551 s, 156 MB/s

\[root@drewserv ~\]\# dd if=/dev/zero of=/dev/md127 count=10000 bs=1M
10000+0 records in 10000+0 records out 10485760000 bytes (10 GB) copied,
71.3196 s, 147 MB/s

Create the filesystem (EXT4)
----------------------------

-   Dry run for fs\*

<!-- -->

    [root@drewserv ~]# mkfs.ext4 -v -E stride=128 -E stripe-width=256 -m 0 -n /dev/vg-raid5/lv-raid5 
    mke2fs 1.41.14 (22-Dec-2010)
    fs_types for mke2fs.conf resolution: 'ext4'
    Calling BLKDISCARD from 0 to 750151270400 failed.
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    Stride=128 blocks, Stripe width=256 blocks
    45793280 inodes, 183142400 blocks
    0 blocks (0.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=4294967296
    5590 block groups
    32768 blocks per group, 32768 fragments per group
    8192 inodes per group
    Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
        4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
        102400000

Real run

    [root@drewserv ~]# mkfs.ext4 -v -E stride=128 -E stripe-width=256 -m 0 /dev/vg-raid5/lv-raid5 
    mke2fs 1.41.14 (22-Dec-2010)
    fs_types for mke2fs.conf resolution: 'ext4'
    Calling BLKDISCARD from 0 to 750151270400 failed.
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    Stride=128 blocks, Stripe width=256 blocks
    45793280 inodes, 183142400 blocks
    0 blocks (0.00%) reserved for the super user
    First data block=0
    Maximum filesystem blocks=4294967296
    5590 block groups
    32768 blocks per group, 32768 fragments per group
    8192 inodes per group
    Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
        4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
        102400000

    Writing inode tables: done                            
    Creating journal (32768 blocks): done
    Writing superblocks and filesystem accounting information: done

    This filesystem will be automatically checked every 34 mounts or
    180 days, whichever comes first.  Use tune2fs -c or -i to override.

### Filesystem Performance Tests

Write test

    [root@drewserv raid5]# dd if=/dev/zero of=/mnt/raid5/10Gtest count=10000 bs=1M
    10000+0 records in
    10000+0 records out
    10485760000 bytes (10 GB) copied, 73.8108 s, 142 MB/s

Read Test

    [root@drewserv raid5]# dd if=/mnt/raid5/10Gtest of=/dev/null count=10000 bs=1M
    10000+0 records in
    10000+0 records out
    10485760000 bytes (10 GB) copied, 85.8405 s, 122 MB/s

    test2 after rebuild
    [drew@drewserv raid5]$ sudo dd if=/dev/zero of=/mnt/raid5/10Gtest bs=1M count=10000
    10000+0 records in
    10000+0 records out
    10485760000 bytes (10 GB) copied, 126.455 s, 82.9 MB/s
    [drew@drewserv raid5]$ sudo dd if=/mnt/raid5/10Gtest of=/dev/null bs=1M count=10000
    10000+0 records in
    10000+0 records out
    10485760000 bytes (10 GB) copied, 76.3866 s, 137 MB/s

### Add to /etc/fstab

    # blkid | grep raid5
    /dev/mapper/vg--raid5-lv--raid5: UUID="16bf772d-bd34-4a14-b314-cea1ed737040" TYPE="ext4" 

    # echo "UUID="16bf772d-bd34-4a14-b314-cea1ed737040" /mnt/raid5 ext4 defaults  1 3" >> /etc/fstab

Restore data from backup
------------------------

Copy data back:

    [root@drewserv ~]# rsync -aqv --log-file=/root/bkup-raid5 /mnt/backup/backup/ /mnt/raid5/
    .
    .
    .
    sent 428464277809 bytes  received 1589811 bytes  27656341.30 bytes/sec
    total size is 428406181021  speedup is 1.00

NOTES NOTES NOTES

<http://en.wikipedia.org/wiki/Mdadm>
<http://www.mythtv.org/wiki/LVM_on_RAID#Performance_Enhancements_.2F_Tuning>

Increasing RAID5 Performance

`   To help RAID5 read/write performance, setting the read-ahead & stripe cache size[2] [3] for the array provides noticeable speed improvements.`  
`       Note: This tip assumes sufficient RAM availability to the system. Insufficient RAM can lead to data loss/corruption`

----sets strip cache----

1.  echo 16384 &gt; /sys/block/md127/md/stripe\_cache\_size

`   ^----- Value in pages per device, i.e. on 4 devices at 8192 comes out to 128MB`

----Sets read-ahead---- / try 32768 , 65536 , 131072 , 262144

1.  blockdev --setra 16384 /dev/md127
2.  blockdev --setra 16384 /dev/video\_vg/video\_lv

<!-- -->

1.  blockdev --setra 16384 /dev/sdb
2.  blockdev --setra 16384 /dev/sdd
3.  blockdev --setra 16384 /dev/sde

///////////////////////////////////////???????????????????

1.  Options used:
2.  blockdev --setra 1536 /dev/md3 (back to default)
3.  cat /sys/block/sd{e,g,i,k}/queue/max\_sectors\_kb
4.  value: 512
5.  value: 512
6.  value: 512
7.  value: 512
8.  Test with, chunksize of raid array (128)
9.  echo 128 &gt; /sys/block/sde/queue/max\_sectors\_kb
10. echo 128 &gt; /sys/block/sdg/queue/max\_sectors\_kb
11. echo 128 &gt; /sys/block/sdi/queue/max\_sectors\_kb
12. echo 128 &gt; /sys/block/sdk/queue/max\_sectors\_kb

<http://www.pcguide.com/ref/hdd/perf/raid/concepts/perfStripe-c.html>
<http://wiki.centos.org/HowTos/Disk_Optimization> For example if you
have 4 drives in RAID5 and it is using 64K chunks and given a 4K file
system block size. The stride size is calculated for the one disk by
(chunk size / block size), (64K/4K) which gives 16. While the stripe
width for RAID5 is 1 disk less, so we have 3 data-bearing disks out of
the 4 in this RAID5 group, which gives us (number of data-bearing drives
\* stride size), (3\*16) gives you a stripe width of 48.

When you create an ext3 partition in this manner, you would format it
like this

mkfs.ext3 -b 4096 -E stride=16 -E stripe-width=48 -O dir\_index
/dev/XXXX

<http://www.nickyeates.com/technology/unix/raid_filesystem_lvm> Note:
You would want to change the stride-width if you added disks to array.

`   tune2fs -E stride=n,stripe-width=m /dev/mdx`
