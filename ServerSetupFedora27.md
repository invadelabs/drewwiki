---
title: ServerSetupFedora27
layout: default
---

Fedora 27 Net Install ISO
=========================

Write to thumb drive
<https://download.fedoraproject.org/pub/fedora/linux/releases/27/Server/x86_64/iso/Fedora-Server-netinst-x86_64-27-1.6.iso>

kickstart.ks
------------

<script src="https://gist.github.com/drew-holt/e00fc2879db092e7c42b4d0101935caf.js">
</script>
Immediate post install steps
============================

Install etckepper and initalize it
----------------------------------

    sudo dnf install etckeeper
    sudo etckeepeer init

Install fail2ban, enable, and start it
--------------------------------------

    sudo dnf install fail2ban
    sudo systemctl enable fail2ban
    sudo systemctl start fail2ban

Disable root login via password ssh
-----------------------------------

    $ grep Root /etc/ssh/sshd_config
    PermitRootLogin prohibit-password

Add TCP/22 to firewalld
-----------------------

Done in kickstart, manually though:

    firewall-cmd --permanent --add-port=80/tcp --add-port=443/tcp
    firewall-cmd --reload

Enable sudo
-----------

User drew is added to wheel in kickstart, manually though:

    $ sudo visudo
    drew    ALL=(ALL) NOPASSWD:ALL

dnf upgrade
-----------

    sudo dnf upgrade -y

Enable SElinux
--------------

Done in kickstart, however:

    $ grep enforcing /etc/selinux/config
    SELINUXTYPE=enforcing
    $ setenforce 1

Extend days of sysstat logging
------------------------------

    $ grep -vE '^($|#)' /etc/sysconfig/sysstat
    HISTORY=365
    COMPRESSAFTER=10
    SADC_OPTIONS=""

Install other software
======================

Do this in kickstart

    # dnf install -y man screen wget strace rsync mailx fdupes logwatch grep lsof screen binutils tar mcelog nfs-utils \
    OpenIPMI ipmitool sysstat clamav clamav-update iscsi-initiator-utils samba openvpn lldpad ntp \
    php-pecl-apc lm_sensors hddtemp smartmontools apcupsd apcupsd-cgi 

Configure system
================

Mail
----

Place holder for postfix config here and firewald rules for TCP25

### add .forward file

    $ sudo echo drew > /root/.forward
    $ sudo echo "andrew: drew" >> /etc/aliases
    $ sudo newaliases
    $ sudo echo "root: drew" >> /etc/aliases
    $ sudo newaliases

Monitoring
----------

Place holder for nagios client config

### Configure lm-sensors

Do this in kickstart

    $ sudo sensors-detect --auto

### lldpad

Do this in kickstart

    $ sudo systemctl enable llpdad
    $ sudo systemctl start llpdad

### mcelog

Do this in kickstart

    systemctl enable mcelog
    systemctl start mcelog

### SMARTmon HDD Alerts

    DEVICESCAN -H -m root -M exec /usr/libexec/smartmontools/smartdnotify -n standby,10,q
    /dev/sda -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdb -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdc -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sdd -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,45 -d sat
    /dev/sde -H -m root -M daily -M exec /home/drew/cron/smartmon.sh -M daily -f -l error -o on -S on -s (S/../.././02|L/../../6/03) -W 0,0,47 -d sat

VPN
---

Place holder for openvpn server

Configure kdump
---------------

Configure apcupsd
-----------------

Time
----

Do this via kickstart. Install chrony and configure, add to firewall
UDP123/24

Rsyslog
-------

Do this via kickstart. For network clients, add UDP514/24 to IPTables

Configure logrotate
-------------------

Do this via kickstart.

    compress

Configure RAID and filesharing
==============================

Mount raid array
----------------

Configure md alerts

Setup clamav
------------

Virus protection for Samba and weekly scan

Enable samba
------------

Add TCP139,445/24 to IPTables

    sudo systemctl enable smb; 
    sudo systemctl start smb

/etc/samba/smb.conf

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

Setup cron jobs
---------------

Keep anacron from waking me up at night!

    $ sudo vi /etc/anacrontab // START_HOURS_RANGE</pre>

Configure Web Services
----------------------

### ddclient for dynamicdns updates

Completing / Wrap-up
====================

-   Verify all log files in /var/log are not giving any errors or
    notifications
-   Check logs for whats growing!
        # ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort -n


