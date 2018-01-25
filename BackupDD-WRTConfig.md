---
title: BackupDD-WRTConfig
layout: default
---

Source
======

Moved to
[GitHub](https://github.com/invadelabs/cron-invadelabs/blob/master/dd-wrt_backup.sh).

Cron
====

``` bash
0 4 * * * cd /mnt/raid5/backup/dd-wrt; wget --user=root --password=admin http://192.168.1.1/nvrambak.bin; mv nvrambak.bin nvrambak.bin`date +%F.%T`;
```
