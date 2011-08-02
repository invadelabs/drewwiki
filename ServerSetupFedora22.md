---
title: ServerSetupFedora22
layout: default
---

    # yum install man screen wget rsync fail2ban mailx fdupes sendmail-cf strace \
    lm_sensors hddtemp apcupsd apcupsd-cgi smartmontools clamav clamav-update nfs-utils \
    logwatch etckeeper OpenIPMI ipmitool sysstat mutt \
    mod_auth_pam mod_auth_shadow php-pecl-apc  gitweb
    # java-1.6.0-openjdk.x86_64 nss-mdns

1.  Install etckeeper
2.  Disable root login via ssh
3.  Enable sudo
4.  Install fail2ban
5.  yum remove unneeded software
6.  yum update
7.  Enable SElinux
8.  Extend days of sysstat logging  
      

<!-- -->

1.  Configure GRUB serial console redirection
2.  Configure kdump for system panics
    1.  Append kernel grub.conf crashkernel=128M for F14
    2.  /etc/sysctl.conf :: kernel.sysrq =1
3.  Configure apcupsd for UPS alerts
4.  Configure Time Server for local network access
    1.  Add UDP 123 to IPTables
5.  Configure syslog for network client writes
    1.  Add UDP 514 to IPTables  
          

<!-- -->

1.  Mount raid array
2.  Configure md alerts
3.  Enable NFS
    1.  Add TCP 2049 to IPTables
    2.  Disable NFSv2/3 /etc/sysconfig/nfs
    3.  $ service rpcbind start ; chkconfig rpcbind on
    4.  $ service nfslock start ; chkconfig nfslock on
    5.  $ service nfs start ; chkconfig nfs on
4.  Enable samba
    1.  Add TCP port 139/445 to IPTables
    2.  1.  chkconfig smb on; chkconfig nmb on;

5.  Enable iSCSI
    1.  Add TCP port 3260
6.  ^ Configure bacula and web interface  
      
7.  Setup mail relay
    1.  $ echo drew &gt; /root/.forward
    2.  echo “andrew: drew” &gt;&gt; /etc/aliases; newaliases
    3.  echo “root: drew” &gt;&gt; /etc/aliases; newaliases
    4.  Remove 127.0.0.1 /etc/mail/sendmail.mc
    5.  Add TCP port 25 to IPTables
8.  Configure smartd to monitor hard drives
9.  ^ Configure thermal alerts for server
10. Configure logwatch
11. Setup clamav virus protection for Samba and weekly scan  
      

<!-- -->

1.  Setup cron jobs
    1.  Keep anacron from waking me up at night! \# vi /etc/anacrontab
        // START\_HOURS\_RANGE  
          
2.  ^ Configure Snort passive IDS
3.  ^ Transparent Proxy with Squid for bandwidth utilization tally  
      
4.  Upload firmware for tv tuner card
5.  Setup mythtv
6.  Configure MythWeb
7.  Force http to https redirection
    1.  Add TCP port 443 to IPTables
8.  Configure MediaWiki
9.  Configure webdav for tomboy notes / foxit marks
10. Configure mod\_auth\_pam for httpd authentication  
      

<!-- -->

1.  ^ Verify all log files in /var/log are not giving any errors or
    notifications
2.  ^ Check logs for whats growing!

:\* ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort
-n
