---
title: ServerSetupFedora22
layout: default
---

`# yum install man screen lm_sensors wget rsync fail2ban mailx sendmail-cf nut clamav clamav-update nfs-utils strace smartmontools logwatch etckeeper OpenIPMI`

1.  Install etckeeper
2.  Disable root login via ssh
3.  Enable sudo
4.  Install fail2ban
5.  yum remove unneeded software
6.  yum update  
      
7.  Configure GRUB serial console redirection
8.  Configure kdump for system panics
9.  Configure NUT for UPS alerts
10. Configure Time Server for local network access
    1.  Add UDP 123 to IPTables
11. Configure syslog for network client writes
    1.  Add UDP 514 to IPTables  
          
12. Mount raid array
13. Configure md alerts
14. Enable NFS
    1.  Add TCP 2049 to IPTables
    2.  Disable NFSv2/3 /etc/sysconfig/nfs
    3.  $ service rpcbind start ; chkconfig rpcbind on
    4.  $ service nfslock start ; chkconfig nfslock on
    5.  $ service nfs start ; chkconfig nfs on
15. Enable samba
    1.  Add TCP port 139/445 to IPTables
16. Enable iSCSI
17. ^ Configure bacula and web interface  
      
18. Setup mail relay
    1.  $ echo drew &gt; /root/.forward
    2.  echo “andrew: drew” &gt;&gt; /etc/aliases; newaliases
    3.  echo “root: drew” &gt;&gt; /etc/aliases; newaliases
    4.  Remove 127.0.0.1 /etc/mail/sendmail.mc
    5.  Add TCP port 25 to IPTables
19. Configure smartd to monitor hard drives
20. ^ Configure thermal alerts for server
21. Configure logwatch
22. Setup clamav virus protection for Samba and weekly scan  
      
23. Setup cron jobs
    1.  Keep anacron from waking me up at night! \# vi /etc/anacrontab
        // START\_HOURS\_RANGE  
          
24. ^ Configure Snort passive IDS
25. ^ Transparent Proxy with Squid for bandwidth utilization tally  
      
26. Upload firmware for tv tuner card
27. Setup mythtv
28. Configure MythWeb
29. Force http to https redirection
    1.  Add TCP port 443 to IPTables
30. Configure webdav for tomboy notes / foxit marks
31. Configure mod\_auth\_pam for httpd authentication  
      
32. ^ Verify all log files in /var/log are not giving any errors or
    notifications
33. ^ Check logs for whats growing!

:\* ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort
-n
