---
title: Ddwrtdnsmasq
layout: default
---

net:2 ---&gt; 3 = gateway

net:2 ---&gt; 6 = DNS

    dhcp-option=net:2,3,192.168.1.5
    dhcp-option=net:2,6,192.168.1.5
    dhcp-host=00:1d:92:61:a1:6f,net:2,192.168.1.70,infinite
    dhcp-host=00:22:64:5E:AD:8B,net:2
    dhcp-host=00:22:15:8C:AF:79,net:2
