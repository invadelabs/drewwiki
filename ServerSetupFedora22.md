---
title: ServerSetupFedora22
layout: default
---

1.  Install etckeeper
2.  Disable root login via ssh
3.  Enable sudo
4.  Install fail2ban
5.  yum remove unneeded software
6.  yum update  
      
7.  Configure grub serial console redirection
8.  Configure serial console via IPMI
9.  Configure kdump for system panics
10. Configure NUT for UPS alerts
11. Configure Time Server for local network access
    1.  Add UDP 123 to IPTables
12. Configure syslog for network client writes
    1.  Add UDP 514 to IPTables  
          
13. Mount raid array
14. Configure md alerts
15. Enable NFS
    1.  Add TCP 2049 to IPTables
    2.  Disable NFSv2/3 /etc/sysconfig/nfs
    3.  $ service rpcbind start ; chkconfig rpcbind on
    4.  $ service nfslock start ; chkconfig nfslock on
    5.  $ service nfs start ; chkconfig nfs on
16. Enable samba
    1.  Add TCP port 139/445 to IPTables
17. Enable iSCSI
18. ^ Configure bacula and web interface  
      
19. Setup mail relay
    1.  $ echo drew &gt; /root/.forward
    2.  echo “andrew: drew” &gt;&gt; /etc/aliases; newaliases
    3.  Add TCP port 25 to IPTables
20. Configure smartd to monitor hard drives
21. ^ Configure thermal alerts for server
22. Configure logwatch
23. Setup clamav virus protection for Samba and weekly scan  
      
24. Setup cron jobs
    1.  Keep anacron from waking me up at night! \# vi /etc/anacrontab
        // START\_HOURS\_RANGE  
          
25. ^ Configure Snort passive IDS
26. ^ Transparent Proxy with Squid for bandwidth utilization tally  
      
27. Upload firmware for tv tuner card
28. Setup mythtv
29. Configure MythWeb
30. Force http to https redirection
    1.  Add TCP port 443 to IPTables
31. Configure webdav for tomboy notes / foxit marks
32. Configure mod\_auth\_pam for httpd authentication  
      
33. ^ Verify all log files in /var/log are not giving any errors or
    notifications
34. ^ Check logs for whats growing!

:\* ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort
-n
