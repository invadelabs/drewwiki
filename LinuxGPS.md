---
title: LinuxGPS
layout: default
---

``` bash
sirfmon /dev/ttyUSB0

sudo gpsd -N -n -D 2 /dev/ttyUSB0
sudo gpsd -N -D 2 /dev/ttyUSB0

sudo gpsd -b -n -N -D 2
```

Import navit maps;

``` bash
bzcat osm_bbox_11.3,47.9,11.7,48.2.osm.bz2 | ../../navit/maptool/maptool --attr-debug-level=5 osm_bbox_11.3,47.9,11.7,48.2.bin.tmp
```
