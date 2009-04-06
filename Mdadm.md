---
title: Mdadm
layout: default
---

### Create md device

Create a raid5 device with 256 chunk size on 4 devices with out any hot
spares.

    # mdadm --create /dev/md0 --level=raid5 --chunk=256 --raid-devices=4 --spare-devices=0 /dev/sd[b-e]

### Create filesystem

#### Ext3

Create an ext3 file system with 0% space reserved for root, a 4096 block
size, and a raid stride of 16 ( 16 \* 256 = 4096 | stride\*chunk=block)

    # mkfs.ext3 -m 0 -b 4096 -E stride=16 /dev/md0

#### Xfs

Install xfs in centos...

    # yum install kmod-xfs xfsdump xfsprogs

Create FS

    # mkfs.xfs /dev/md0

Need to research tunable fs parameters.

### Performance Testing

#### Bonnie++

    # bonnie++ -d /mnt/raid5/tmp -u drew -f

#### Iozone

-a auto -b output\_excel file -i run read test -i run write test

    # iozone -a -b werd.xls -i 0 -i 1 -C -E

### Additional Tunables

=

    # This step must come first.
    # See: http://www.3ware.com/KB/article.aspx?id=11050

    echo "Setting max_sectors_kb to chunk size of RAID5 arrays..."
    for i in sdc sdd sde sdf sdg sdh sdi sdj sdk sdl
    do
       echo "Setting /dev/$i to 128K..."
       echo 128 > /sys/block/"$i"/queue/max_sectors_kb
    done

    echo "Setting read-ahead to 64MB for /dev/md3"
    blockdev --setra 65536 /dev/md3

    echo "Setting stripe_cache_size to 16MB for /dev/md3"
    echo 16384 > /sys/block/md3/md/stripe_cache_size

    # if you use more than the default 64kb stripe with raid5
    # this feature is broken so you need to limit it to 30MB/s
    # neil has a patch, not sure when it will be merged.
    echo "Setting minimum and maximum resync speed to 30MB/s..."
    echo 30000 > /sys/block/md0/md/sync_speed_min
    echo 30000 > /sys/block/md0/md/sync_speed_max
    echo 30000 > /sys/block/md1/md/sync_speed_min
    echo 30000 > /sys/block/md1/md/sync_speed_max
    echo 30000 > /sys/block/md2/md/sync_speed_min
    echo 30000 > /sys/block/md2/md/sync_speed_max
    echo 30000 > /sys/block/md3/md/sync_speed_min
    echo 30000 > /sys/block/md3/md/sync_speed_max

    # Disable NCQ.
    echo "Disabling NCQ..."
    for i in sdc sdd sde sdf sdg sdh sdi sdj sdk sdl
    do
       echo "Disabling NCQ on $i"
       echo 1 > /sys/block/"$i"/device/queue_depth
    done