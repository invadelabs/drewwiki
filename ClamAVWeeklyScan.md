---
title: ClamAVWeeklyScan
layout: default
---

Run weekly at 3am on Friday

    0 3 * * 5 clamscan -i --no-archive /mnt/raid5/ | mail -s "drew-desktop: ClamAV Scan" example@example.com;

-   --no-archive is probably a bad idea
