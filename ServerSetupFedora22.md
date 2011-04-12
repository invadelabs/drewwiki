---
title: ServerSetupFedora22
layout: default
---

1.  Disable root login via ssh
2.  Enable sudo
3.  Install fail2ban
4.  yum remove unneeded software
5.  yum update  
      
6.  Configure grub serial console redirection
7.  Configure serial console via IPMI
8.  Configure kdump for system panics
9.  Configure NUT for UPS alerts
10. Configure Time Server for local network access
11. Configure syslog for network client writes
    1.  Add UDP 514 in IPTables
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
19. Configure smartd to monitor hard drives
20. ^ Configure thermal alerts for server
21. Configure logwatch
22. Setup clamav virus protection for Samba and weekly scan  
      
23. Setup cron jobs  
      
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
