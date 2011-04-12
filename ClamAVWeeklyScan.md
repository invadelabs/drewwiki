---
title: ClamAVWeeklyScan
layout: default
---

Run weekly at 3am on Friday

    0 3 * * 5 clamscan --scan-archive=no -i -r /mnt/raid5/ | mail -s "drew-desktop: ClamAV Scan" drewderivative@gmail.com;

-   --scan-archive=no is probably a bad idea

