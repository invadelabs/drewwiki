---
title: PortMirroringDDWRTiptables
layout: default
---

    iptables -A PREROUTING -t mangle -j ROUTE --gw 192.168.15.20 --tee
    iptables -A POSTROUTING -t mangle -j ROUTE --gw 192.168.15.20 --tee