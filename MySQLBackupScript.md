---
title: MySQLBackupScript
layout: default
---

The Script
----------

Moved to
[GitHub](https://github.com/invadelabs/cron-invadelabs/blob/master/mysql_backup.sh)

-   Need to get pw off console command

Crontab Entry
-------------

/etc/crontab;

``` bash
0 4     * * *   drew    /home/drew/cron/mysql_backup.sh >> /home/drew/cron/mysql_backup.log;
```
