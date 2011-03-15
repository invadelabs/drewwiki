---
title: SambaTdbsamBackend
layout: default
---

/etc/samba/smb.conf

    [global]
            workgroup = LOCALNET
            server string = dr3w s3rv
            passdb backend = tdbsam
            log file = /var/log/samba/log.%m
            max log size = 50
            load printers = no
            printcap name = /etc/printcap

    [raid5]
            path = /mnt/raid5/drew
            valid users = drew
            read only = No

    [share]
            path = /mnt/raid5
            valid users = user,drew
            read only = No

    [iso]
            path = /mnt/iso
            guest ok = Yes
            read only = Yes

    [video]
            path = /mnt/raid5/drew/video/
            guest ok = Yes
            read only = Yes
