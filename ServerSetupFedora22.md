---
title: ServerSetupFedora22
layout: default
---

**To-do:** This page is outdated and needs better formatting.

Immediate post install steps
============================

Install etckepper and fail2ban
------------------------------

Initalize and ensure service is running

    sudo yum install etckeeper fail2ban
    sudo etckeepeer init
    sudo systemctl enable fail2ban
    sudo systemctl start fail2ban

Disable root login via password ssh
-----------------------------------

    $ grep Root /etc/ssh/sshd_config
    PermitRootLogin prohibit-password

Add TCP22/0 to IPTables
-----------------------

Enable sudo
-----------

    $ sudo grep drew /etc/sudoers
    drew    ALL=(ALL) NOPASSWD:ALL

yum remove unneeded software
----------------------------

yum update
----------

Enable SElinux
--------------

Extend days of sysstat logging
------------------------------

    $ grep -vE '^($|#)' /etc/sysconfig/sysstat
    HISTORY=365
    COMPRESSAFTER=10
    SADC_OPTIONS=""

Install rest of software
========================

    # yum install man screen wget strace rsync mailx fdupes logwatch grep lsof screen binutils tar mcelog nfs-utils \
    OpenIPMI ipmitool sysstat clamav clamav-update iscsi-initiator-utils samba openvpn lldpad ntp \
    php-pecl-apc lm_sensors hddtemp smartmontools apcupsd apcupsd-cgi 

Configure system, monitoring, mail, AV, and VPN
===============================================

1.  Configure GRUB serial console redirection
2.  Configure kdump for system panics
3.  Configure lm-sensors, smartd/hddtemp+thermal alerts, lldpad, mcelog,
    and SMARTmon for temperature alerts.
    1.  1.  

<!-- -->

     DEVICESCAN -H -m root -M exec /usr/libexec/smartmontools/smartdnotify -n standby,10,q
    /dev/sda -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdb -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdc -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdd -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sde -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,47 -d sat

1.  Configure apcupsd for UPS alerts
2.  Configure Time Server for local network access
    1.  Add UDP123/24 to IPTables
3.  Configure rsyslog for network clients
    1.  Add UDP514/24 to IPTables
4.  Setup mail relay
    1.  Remove 127.0.0.1 /etc/mail/sendmail.mc
    2.  # echo drew > /root/.forward; echo "andrew: drew" >> /etc/aliases; newaliases; echo "root: drew" >> /etc/aliases; newaliases

    3.  Add TCP25/0 to IPTables

5.  Configure logwatch
6.  Setup clamav virus protection for Samba and weekly scan
7.  Configure OpenVPN

Configure RAID and filesharing
==============================

1.  Mount raid array
2.  Configure md alerts
3.  Enable samba
    1.  Add TCP139,445/24 to IPTables
    2.  # systemctl enable smb; systemctl start smb

        1.  

<!-- -->

     
    [global]
            workgroup = WORKGROUP
            server string = drewserv
            security = user
            passdb backend = tdbsam
            log file = /var/log/samba/log.%m
            max log size = 50
            load printers = no
            show add printer wizard = no
            printcap name = /dev/null
            disable spoolss = yes
    [share]
            path = /mnt/raid5
            valid users = drew pbr
            read only = No
        create mode = 0665
        directory mode = 0775

1.  Enable iSCSI
    1.  Add TCP3260/24
2.  ^ Configure bacula and web interface

Setup cron jobs
===============

1.  Keep anacron from waking me up at night!

<!-- -->

    # vi /etc/anacrontab // START_HOURS_RANGE

Configure Web Services
======================

1.  ddclient for dynamicdns updates
2.  Configure MythTV / MythWeb / minidlna
    1.  Add TCP80/24 and TCP443/0 for web services, TCP1900/0 TCP8200/0,
        TCP34531/0 for minidlna
        1.  

<!-- -->

     
    port=8200
    media_dir=/mnt/raid5/media
    db_dir=/var/cache/minidlna
    log_dir=/var/log/minidlna
    album_art_names=Cover.jpg/cover.jpg/AlbumArtSmall.jpg/albumartsmall.jpg/AlbumArt.jpg/albumart.jpg/Album.jpg/album.jpg/Folder.jpg/folder.jpg/Thumb.jpg/thumb.jpg
    inotify=yes
    enable_tivo=no
    strict_dlna=no
    notify_interval=900
    serial=12345678
    model_number=1
    root_container=B

1.  Configure pecl-php-apc / DrewWiki / WebDAV

Completing / Wrap-up
====================

1.  Verify all log files in /var/log are not giving any errors or
    notifications
2.  Check logs for whats growing!
        # ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort -n

3.  Create MondoRescue restore image

