---
title: ServerSetupFedora22
layout: default
---

    # yum install man screen wget strace rsync fail2ban mailx mutt fdupes sendmail-cf logwatch etckeeper \
    OpenIPMI ipmitool sysstat clamav clamav-update nfs-utils iscsi-initiator-utils samba \
    mod_auth_pam mod_auth_shadow php-pecl-apc phpMyAdmin \
    lm_sensors hddtemp smartmontools apcupsd apcupsd-cgi 
    # java-1.6.0-openjdk.x86_64 nss-mdns

1.  Install etckeeper
2.  Disable root login via ssh
    1.  Add TCP22/0 to IPTables
3.  Enable sudo
4.  Install fail2ban
5.  yum remove unneeded software
6.  yum update
7.  Enable SElinux
8.  Extend days of sysstat logging

<!-- -->

1.  Configure GRUB serial console redirection
2.  Configure kdump for system panics
3.  Configure lm-sensors, hddtemp, and SMARTmon for temperature alerts.
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

<!-- -->

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

<!-- -->

1.  Setup cron jobs
    1.  Keep anacron from waking me up at night!
            # vi /etc/anacrontab // START_HOURS_RANGE

<!-- -->

1.  Configure MythTV / MythWeb
    1.  Add TCP443/0 to IPTables
2.  Configure mod\_auth\_pam / mod\_auth\_shadow / pecl-php-apc /
    phpMyAdmin
3.  Configure DrewWiki / WebDAV

<!-- -->

1.  Verify all log files in /var/log are not giving any errors or
    notifications
2.  Check logs for whats growing!
        # ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort -n


