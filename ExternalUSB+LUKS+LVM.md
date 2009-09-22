---
title: ExternalUSB+LUKS+LVM
layout: default
---

Format the drive for encryption, supply pass or key..

    # cryptsetup luksFormat /dev/sdb

Open and mount the drive, it will be available at /dev/mapper/external

    # cryptsetup luksOpen /dev/sdb external

Create LVM (PV, VG, LV), format as ext4 reserving 0% for root, and mount
the drive.

    # pvcreate /dev/mapper/external
    # vgcreate vg-backup /dev/mapper/external
    # lvcreate -l 17884 vg-backup
    # mkfs.ext4 -m 0 /dev/vg-backup/lvol0
    # mount /dev/vg-backup/lvol0 /mnt/backup

To unmount;

    # umount /mnt/backup
    # lvchange -a n /dev/vg-backup/lvol0
    # vgchange -a n vg-backup
    # cryptsetup luksClose /dev/mapper/external

To mount;

    # cryptsetup luksOpen /dev/sdb
    <pre># mount /dev/vg-backup/lvol0 /mnt/backup

Research: What is the best way to remove LVM's left over device files.

Rsync backup; This is a **dry run** which will delete files not on the
source, log everything to ~/backup.log, exclude a video directory from
all files named /mnt/raid5 to /mnt/backup.

    # rsync -avn --delete --log-file=/root/raid5_backup.log --exclude drew/video /mnt/raid5/ /mnt/backup

The real deal.

    # rsync -av --delete --log-file=/root/raid5_backup.log --exclude drew/video /mnt/raid5/ /mnt/backup
