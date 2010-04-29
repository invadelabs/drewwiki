---
title: NUTUPSMonitor
layout: default
---

1. Install network ups tool;

    # yum install nut nut-client

2. Change mode from none -&gt; standalone in /etc/ups/nut.conf

    #MODE = none
    MODE = standalone

3. Add a UPS device in /etc/ups/ups.conf;

-   Use auto for port if USB

<!-- -->

    [drewups]
            driver=usbhid-ups
            port = auto
            desc = "Office UPS"

4. Create a master to use to communicate with nut in
/etc/ups/upsd.users;

    [amasteruser]
           password = anawesomepassword
           upsmon master

5. Configure /etc/ups/upsmon.conf to monitor drewups as amasteruser, run
a script when an action occurs, as well as alert;

    MONITOR drewups@localhost 1 amasteruser anawesomepassword master

    NOTIFYCMD /home/drew/cron/upspager.sh

    NOTIFYFLAG ONLINE       SYSLOG+EXEC+WALL
    NOTIFYFLAG ONBATT       SYSLOG+EXEC+WALL
    NOTIFYFLAG LOWBATT      SYSLOG+EXEC+WALL
    NOTIFYFLAG FSD          SYSLOG+EXEC+WALL
    NOTIFYFLAG COMMOK       SYSLOG+EXEC+WALL
    NOTIFYFLAG COMMBAD      SYSLOG+EXEC+WALL
    NOTIFYFLAG SHUTDOWN     SYSLOG+EXEC+WALL
    NOTIFYFLAG REPLBATT     SYSLOG+EXEC+WALL
    NOTIFYFLAG NOCOMM       SYSLOG+EXEC+WALL
    NOTIFYFLAG NOPARENT     SYSLOG+EXEC+WALL

6. upspager.sh script;

    #!/bin/bash
    echo "$*" | mail -s "drewups alert" me+alerts@gmail.com

7. Start nut at boot and fire it up;

    # chkconfig ups on
    # /etc/init.d/ups start
