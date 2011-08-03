---
title: Lm sensorsPDMSi
layout: default
---

    # cat /etc/sensors.d/pdsmi
    chip "w83792d-*"
        ignore temp1
        ignore fan1
        ignore fan2
        ignore fan3
        ignore fan4

        label in0 "Vcore"
        #label in1  "1.5V"
        #label fan5 "CPU Fan" # ?
        #label fan6 "CPU Fan" # ?
        label temp2 "CPU Temp"
        label temp3 "System Temp"
