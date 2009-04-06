---
title: NFS Optimization
layout: default
---

### Server Side

#### /etc/exports

    /mnt/raid5 192.168.15.142/32(rw,async,no_root_squash)

async - dramatic throughput increase, but dangerous if a client does not
unmount cleanly..

#### Tuning /etc/sysctl.conf

          net.core.rmem_default = 262144
          net.core.rmem_max = 262144
          #
          # Increase the fragmented packet queue length
          net.ipv4.ipfrag_high_thresh = 524288
          net.ipv4.ipfrag_low_thresh = 393216

echo 0 &gt; /proc/sys/net/ipv4/tcp\_sack echo 0 &gt;
/proc/sys/net/ipv4/tcp\_timestamps

#### TCP Segmentation offload

This will take off some of the tcp overhead if your card supports it..

    # ethtool -K ethN tso on

### Client Side

##### /etc/fstab

    192.168.15.20:/mnt/raid5 /mnt/raid5 nfs rsize=32768,wsize=32768,intr,hard 0 0

\[rw\]size=32768 - NFSv3 maximum read write size intr - if the mount
drops, you'll still be able to ^C out of whatever operation your running
hard - hm?