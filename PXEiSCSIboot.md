---
title: PXEiSCSIboot
layout: default
---

    dhcp-match=gpxe,175
    dhcp-boot=net:#gpxe,gpxe.pxe,drewserv,192.168.15.20
    #dhcp-boot=menu.gpxe,drewserv,192.168.15.20
    #dhcp-boot=http://192.168.15.20/drew/menu.gpxe
    #dhcp-option=175,8:1:1 # keep-san
    dhcp-option=17,"iscsi:192.168.15.20::::iqn.2009-11.local.drew-desktop:storage.lun1"