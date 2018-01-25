---
title: SambaTdbsamBackend
layout: default
---

``` bash
[root@drewserv ~]# cat /etc/samba/smb.conf
[global]
        workgroup = WORKGROUP
        server string = drewserv
    security = user
        passdb backend = tdbsam
        log file = /var/log/samba/log.%m
        max log size = 50

;   Get samba to stop complaining about cups
        load printers = no
    show add printer wizard = no
    printcap name = /dev/null
    disable spoolss = yes

[share]
        path = /mnt/raid5
        valid users = user,drew
        read only = No
```
