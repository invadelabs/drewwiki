---
title: ServerSetupFedora22
layout: default
---

Immediate post install steps
============================

1.  sudo yum install etckeeper fail2ban

2.  Disable root login via ssh
    1.  Add TCP22/0 to IPTables
3.  Enable sudo
4.  yum remove unneeded software
5.  yum update
6.  Enable SElinux
7.  Extend days of sysstat logging

Install rest of software
========================

    # yum install man screen wget strace rsync mailx fdupes logwatch grep lsof screen binutils tar mcelog nfs-utils \
    OpenIPMI ipmitool sysstat clamav clamav-update nfs-utils iscsi-initiator-utils samba openvpn lldpad ntp \
    php-pecl-apc lm_sensors hddtemp smartmontools apcupsd apcupsd-cgi 

Configure system, monitoring, mail, AV, and VPN
===============================================

1.  Configure GRUB serial console redirection
2.  Configure kdump for system panics
3.  Configure lm-sensors, hddtemp, lldpad, mcelog, and SMARTmon for
    temperature alerts.
4.  Configure apcupsd for UPS alerts
5.  Configure Time Server for local network access
    1.  Add UDP123/24 to IPTables
6.  Configure rsyslog for network clients
    1.  Add UDP514/24 to IPTables
7.  Setup mail relay
    1.  Remove 127.0.0.1 /etc/mail/sendmail.mc
    2.  # echo drew > /root/.forward; echo "andrew: drew" >> /etc/aliases; newaliases; echo "root: drew" >> /etc/aliases; newaliases

    3.  Add TCP25/0 to IPTables

8.  Configure smartd/hddtemp for disk monitoring
9.  ^ Configure thermal alerts for server
10. Configure logwatch
11. Setup clamav virus protection for Samba and weekly scan
12. Configure OpenVPN

Configure RAID and filesharing
==============================

1.  Mount raid array
2.  Configure md alerts
3.  Enable NFS
    1.  Add TCP2049/24 to IPTables
    2.  Disable NFSv2/3 /etc/sysconfig/nfs
4.  Enable samba
    1.  Add TCP139,445/24 to IPTables
    2.  # chkconfig smb on; chkconfig nmb on;

5.  Enable iSCSI
    1.  Add TCP3260/24
6.  ^ Configure bacula and web interface

Setup cron jobs
===============

1.  Keep anacron from waking me up at night!

<!-- -->

    # vi /etc/anacrontab // START_HOURS_RANGE

Configure Web Services
======================

1.  Configure MythTV / MythWeb / minidlna
    1.  Add TCP443/0 to IPTables
2.  Configure pecl-php-apc / DrewWiki / WebDAV

Completing / Wrap-up
====================

1.  Verify all log files in /var/log are not giving any errors or
    notifications
2.  Check logs for whats growing!
        # ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort -n

3.  Create MondoRescue restore image

