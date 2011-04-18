---
title: Iptables
layout: default
---

For desktop host, only allow tunnel

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

On router

    iptables -I INPUT 1 -s 192.168.1.142 -p udp --dport 53 -j REJECT
    iptables -I FORWARD 1 -s 192.168.1.142 -d 70.87.42.50 -p tcp --dport 1123 -j ACCEPT
    iptables -I FORWARD 2 -s 192.168.1.142 -j REJECT
