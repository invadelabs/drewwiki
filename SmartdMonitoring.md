---
title: SmartdMonitoring
layout: default
---

    [root@drewserv ~]# grep -v ^# /etc/smartd.conf  | grep -v ^$
    [root@drewserv etc]# grep -v ^$ /etc/smartd.conf | grep -v ^#
    /dev/sda -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
    /dev/sdb -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
    /dev/sdc -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
    /dev/sdd -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
    /dev/sde -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
    /dev/sdf -H -m root -M daily -M exec  /home/drew/cron/smartmon.sh -a -o on -S on -s (S/../.././02|L/../../6/03) -W 10 -d sat
