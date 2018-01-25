---
title: Udevinfo
layout: default
---

Rules /etc/udev/rules.d

``` bash
cd /sys/class/net/eth0
udevinfo -p `pwd` -a
```
