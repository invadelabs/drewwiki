---
title: BackupPartitionsViaDDandSfdisk
layout: default
---

Backup first 446, then windows partitions..

``` bash
# sfdisk -d /dev/sda > drew-8570w-win10_sfdisk
# dd if=/dev/sda of=drew-8570w-win10.bs446 bs=446 count=1
# dd if=/dev/sda1 of=drew-8570w-win10.sda1
# dd if=/dev/sda2 of=drew-8570w-win10.sda2
# dd if=/dev/sda3 of=drew-8570w-win10.sda3
# dd if=/dev/sda4 of=drew-8570w-win10.sda4
```
