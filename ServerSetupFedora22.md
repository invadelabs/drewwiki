---
title: ServerSetupFedora22
layout: default
---

    1. Disable root login via ssh
    2. Enable sudo
    3. yum remove unneeded software
    4. yum update

    5. Configure grub serial console redirection
    6. Configure serial console via IPMI
    7. Configure kdump for system panics
    8. Configure NUT for UPS alerts
    9. Configure Time Server for local network access
    10. Configure syslog for network client writes

    11. Mount raid array
    12. Configure md alerts
    13. Enable NFS
    14. Enable samba
    15. Enable iSCSI
    16. Configure bacula and web interface

    17. Setup mail relay
    18. Configure smartd to monitor hard drives
    ^19. Configure thermal alerts for server
    20. Configure logwatch
    21. Setup clamav virus protection for Samba and weekly scan

    22. Setup cron jobs

    23. Configure denyhosts or fail2ban
    24. Configure Snort passive IDS
    25. Transparent Proxy with Squid for bandwidth utilization tally

    25. Upload firmware for tv tuner card
    26. Setup mythtv
    27. Configure MythWeb
    28. Force http to https redirection

    29. Configure webdav for tomboy notes / foxit marks

    ^30. Configure SElinux

    ^31. Verify all log files in /var/log are not giving any errors or notifications
    ^32. Check logs for whats growing!
    # ls -alR /var/log | grep ^- | awk {'print $5" "$8'} | sort -k 2| sort -n
