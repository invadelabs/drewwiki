---
title: IPMI
layout: default
---

    # grub.conf generated by anaconda
    #
    # Note that you do not have to rerun grub after making changes to this file
    # NOTICE:  You have a /boot partition.  This means that
    #          all kernel and initrd paths are relative to /boot/, eg.
    #          root (hd0,0)
    #          kernel /vmlinuz-version ro root=/dev/VolGroup00/LogVol00
    #          initrd /initrd-version.img
    #boot=/dev/sda

    # Redirect grub output to serial console, which is on COM Port 2
    serial --unit=1 --speed=19200 --word=8 --parity=no --stop=1   
    terminal --timeout=10 serial console

    default=0
    timeout=10

    # making IPMI friendly
    #splashimage=(hd0,0)/grub/splash.xpm.gz
    #hiddenmenu

    title CentOS (2.6.18-92.1.22.el5)
        root (hd0,0)
        kernel /vmlinuz-2.6.18-92.1.22.el5 ro root=/dev/VolGroup00/LogVol00 console=ttyS1,19200n8 console=tty0
        initrd /initrd-2.6.18-92.1.22.el5.img
    title CentOS (2.6.18-92.el5)
        root (hd0,0)
        kernel /vmlinuz-2.6.18-92.el5 ro root=/dev/VolGroup00/LogVol00 console=tty0 console=ttyS1,19200n8
        initrd /initrd-2.6.18-92.el5.img
    title "My bios update"
        kernel /memdisk
        initrd /fwdisk.img floppy