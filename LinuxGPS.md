---
title: LinuxGPS
layout: default
---

    sirfmon /dev/ttyUSB0

    sudo gpsd -N -n -D 2 /dev/ttyUSB0
    sudo gpsd -N -D 2 /dev/ttyUSB0

    sudo gpsd -b -n -N -D 2
