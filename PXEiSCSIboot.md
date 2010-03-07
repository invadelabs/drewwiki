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

    # chain booting
      enable-tftp
      tftp-root=/var/lib/tftpboot    # place your gpxe.pxe (either built yourself or from <link:url>http://rom-o-matic.net</link:url> here)
      dhcp-match=gpxe,175            # tags the request with net:gpxe if the gPXE option was supplied in DHCP request
      dhcp-option=175,8:1:1          # turn on the keep-san option to allow installation
      dhcp-boot=net:#gpxe,gpxe.pxe   # Here #gpxe means 'not gpxe': that is the tag is not set
      dhcp-option=net:gpxe,17,"iscsi:ta.rg.et.ip::::iqn.yyyy-mm.reversed-domain-name:identifier"

    option space gpxe;
    option gpxe-encap-opts code 175 = encapsulate gpxe;
    option gpxe.bus-id code 177 = string;
      
    group {
      host iscsihost {
        hardware ethernet 00:0c:29:01:02:03;
        fixed-address iscsihost.mydomain.org;

        if not exists gpxe.bus-id {
            filename "undionly.kpxe";
        } else {
            filename="";
            option root-path "iscsi:192.168.0.10::::iqn.1987-05.com.cisco:lvol1";
        }
      }
    }
