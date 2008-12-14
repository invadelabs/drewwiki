---
title: BackupDD-WRTConfig
layout: default
---

    0 4 * * * cd /mnt/raid5/backup/dd-wrt; wget --user=root --password=admin http://192.168.1.1/nvrambak.bin; mv nvrambak.bin nvrambak.bin`date +%F.%T`;
