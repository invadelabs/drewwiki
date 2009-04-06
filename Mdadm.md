---
title: Mdadm
layout: default
---

raid chunk size set to 64k

1.  mdadm --create /dev/md0 --level=raid5 --chunk=256 --raid-devices=4
    --spare-devices=0 /dev/sd\[b-e\]

<!-- -->

1.  yum install kmod-xfs xfsdump xfsprogs

<!-- -->

1.  mkfs.ext3 -m 0 -b 4096 -E stride=16 /dev/mapper/sil\_ajaeadddahbg
2.  bonnie++ -d /mnt/raid5/tmp -u drew -f

-a auto -b output\_excel file -i run read test -i run write test

1.  iozone -a -b werd.xls -i 0 -i 1 -C -E

<!-- -->

1.  This step must come first.
2.  See: <http://www.3ware.com/KB/article.aspx?id=11050>

echo “Setting max\_sectors\_kb to chunk size of RAID5 arrays...” for i
in sdc sdd sde sdf sdg sdh sdi sdj sdk sdl do

`  echo `“`Setting`` ``/dev/$i`` ``to`` ``128K...`”  
`  echo 128 > /sys/block/`“`$i`”`/queue/max_sectors_kb`

done

echo “Setting read-ahead to 64MB for /dev/md3” blockdev --setra 65536
/dev/md3

echo “Setting stripe\_cache\_size to 16MB for /dev/md3” echo 16384 &gt;
/sys/block/md3/md/stripe\_cache\_size

1.  if you use more than the default 64kb stripe with raid5
2.  this feature is broken so you need to limit it to 30MB/s
3.  neil has a patch, not sure when it will be merged.

echo “Setting minimum and maximum resync speed to 30MB/s...” echo 30000
&gt; /sys/block/md0/md/sync\_speed\_min echo 30000 &gt;
/sys/block/md0/md/sync\_speed\_max echo 30000 &gt;
/sys/block/md1/md/sync\_speed\_min echo 30000 &gt;
/sys/block/md1/md/sync\_speed\_max echo 30000 &gt;
/sys/block/md2/md/sync\_speed\_min echo 30000 &gt;
/sys/block/md2/md/sync\_speed\_max echo 30000 &gt;
/sys/block/md3/md/sync\_speed\_min echo 30000 &gt;
/sys/block/md3/md/sync\_speed\_max

1.  Disable NCQ.

echo “Disabling NCQ...” for i in sdc sdd sde sdf sdg sdh sdi sdj sdk sdl
do

`  echo `“`Disabling`` ``NCQ`` ``on`` ``$i`”  
`  echo 1 > /sys/block/`“`$i`”`/device/queue_depth`

done
