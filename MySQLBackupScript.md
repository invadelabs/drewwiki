---
title: MySQLBackupScript
layout: default
---

The Script
----------

    #!/bin/sh
    USER=some_user
    PW=some_pw
    DIR=/mnt/raid5/backup/mysql

    echo Running: `date`;

    mkdir -vp $DIR;

    mysqldump -u$USER -p$PW --all-databases | gzip > $DIR/mysql.`hostname`.`date +%F.%T`.sql.gz;

    # delete backups older than 30 days
    find $DIR -type f -mtime +30 -exec rm -v {} \;

Crontab Entry
-------------

/etc/crontab;

    0 4    * * *   drew    /home/drew/cron/mysql_backup.sh >> /home/drew/cron/mysql_backup.log;

OR

crontab -e;

    0 4 * * *  /home/drew/cron/mysql_backup.sh >> /home/drew/cron/mysql_backup.log;
