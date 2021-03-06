---
title: Iptables
layout: default
---

For desktop host, only allow tunnel
===================================

``` bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state NEW -p tcp --dport ssh -j ACCEPT
iptables -A INPUT -j REJECT

iptables -A FORWARD -j DROP

iptables -A OUTPUT -p udp  --dport 53 -j REJECT
iptables -A OUTPUT -d 192.168.1.0/24 -j ACCEPT
iptables -A OUTPUT -d *forwarding_host_ip*/32 -j ACCEPT
iptables -A OUTPUT -d 0.0.0.0/0 -j REJECT
```

On router
=========

``` bash
iptables -I INPUT 1 -s 192.168.1.142 -p udp --dport 53 -j REJECT
iptables -I FORWARD 1 -s 192.168.1.142 -d 70.87.42.50 -p tcp --dport 1123 -j ACCEPT
iptables -I FORWARD 2 -s 192.168.1.142 -j REJECT
```

Server
======

``` bash
cat /etc/sysconfig/iptables
# Firewall configuration written by system-config-firewall
# Manual customization of this file is not recommended.
*filter
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -i lo -j ACCEPT

-A INPUT -m state --state NEW -m tcp -p tcp --dport 22 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 25 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT

-A INPUT -m state --state NEW -m udp -p udp -s 192.168.1.0/24 --dport 123 -j ACCEPT
-A INPUT -m state --state NEW -m udp -p udp -s 192.168.1.0/24 --dport 514 -j ACCEPT

-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.1.0/24 --dport 139 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.1.0/24 --dport 445 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.1.0/24 --dport 2049 -j ACCEPT

-A INPUT -j REJECT --reject-with icmp-host-prohibited
-A FORWARD -j REJECT --reject-with icmp-host-prohibited
COMMIT
```
