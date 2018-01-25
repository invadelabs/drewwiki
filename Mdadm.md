---
title: Mdadm
layout: default
---

### Software RAID

#### Create md device

Create a raid5 device with 256 chunk size on 4 devices with out any hot
spares.

``` bash
# mdadm --create /dev/md0 --level=raid5 --chunk=256 --raid-devices=4 --spare-devices=0 /dev/sd[b-e]
```

#### Create /etc/mdadm.conf

``` bash
# mdadm  --examine  --scan --config=mdadm.conf >> /etc/mdadm.conf
```

Modify as appropriate, ex;

``` bash
DEVICE partitions
CREATE owner=root group=disk mode=0660 auto=yes
HOMEHOST <system>
MAILADDR root
```

#### Replace dead device

``` bash
# mdadm /dev/md0 -a /dev/sdc
```

#### Force a degraded array to start

If a drive fails, reboot happens, and we need to restart an array with 3
out of 4 drives running

``` bash
# mdadm -Af /dev/md0 -Af /dev/md0 /dev/sda /dev/sdb /dev/sdd
```

### Create filesystem

#### Ext3

Create an ext3 file system with 0% space reserved for root, a 4096 block
size, and a raid stride of 16 ( 16 \* 256 = 4096 | stride\*chunk=block)

``` bash
# mkfs.ext3 -m 0 -b 4096 -E stride=16 /dev/md0
```

### Performance Testing

#### Bonnie++

``` bash
# bonnie++ -d /mnt/raid5/tmp -u drew -f
```

#### Iozone

-   -a auto
-   -b output\_excel file
-   -i 0 run read test
-   -i 1 run write test

``` bash
# iozone -a -b werd.xls -i 0 -i 1 -C -E
```

### Additional Tunables

Most of this were pulled from
<http://www.3ware.com/KB/article.aspx?id=11050>

#### max\_sectors\_kb

``` bash
echo "Setting max_sectors_kb to chunk size of RAID5 arrays..."
for i in sdb sdc sdd sde
do
   echo "Setting /dev/$i to 128K..."
   echo 128 > /sys/block/"$i"/queue/max_sectors_kb
done
```

#### Read-ahead on md0

-   I hear this eats a lot of RAM

``` bash
echo "Setting read-ahead to 64MB for /dev/md3"
blockdev --setra 65536 /dev/md0
```

#### stripe\_cache\_size

-   + stripe\_cache\_size (raid4, raid5 and raid6)
-   number of entries in the stripe cache. This is writable, but there
    are upper and lower limits (32768, 16). Default is 128.
-   + stripe\_cache\_active (raid4, raid5 and raid6)
-   number of active entries in the stripe cache

<!-- -->

-   + The stripe cache memory is locked down and not available for other
    uses.
-   + The total size of the stripe cache is determined by this formula:
-   +
-   + PAGE\_SIZE \* raid\_disks \* stripe\_cache\_size = memory used

``` bash
echo "Setting stripe_cache_size to 16MB for /dev/md3"
echo 16384 > /sys/block/md0/md/stripe_cache_size
```

#### Array resync speed

-   Dramatically improves resync performance...

``` bash
# Increase the minimum / maximum resync speed of the array..
echo "Setting minimum and maximum resync speed to 100MB/s..."
echo 100000 > /sys/block/md0/md/sync_speed_min
echo 100000 > /sys/block/md0/md/sync_speed_max
```

#### Disable NCQ

-   Disabling native command queuing ... Benefits?

``` bash
# Disable NCQ.
echo "Disabling NCQ..."
for i in sdc sdd sde sdf sdg sdh sdi sdj sdk sdl
do
   echo "Disabling NCQ on $i"
   echo 1 > /sys/block/"$i"/device/queue_depth
done
```
