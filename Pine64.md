---
title: Pine64
layout: default
---

``` bash
/usr/local/sbin/resize_rootfs.sh
- fix end sector to minus one in script >.<
- sunxi-disp-tool -screen 0 switch 2 # https://github.com/longsleep/sunxi-disp-tool
- https://www.pine64.pro/getting-started-linux/
- sudo dd if=/dev/zero of=/var/swap bs=1M count=1024
- mkswap /var/swap
- swap on /var/swap
- add to /etc/fstab
```
