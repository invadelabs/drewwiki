---
title: ClamAVWeeklyScan
layout: default
---

Run weekly at 3am on Friday

``` bash
0 3 * * 5 clamscan --scan-archive=no -i -r /mnt/raid5/ | mail -s "drew-desktop: ClamAV Scan" drew@invadelabs.com;
```

-   --scan-archive=no is probably a bad idea

