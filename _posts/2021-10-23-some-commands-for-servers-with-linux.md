---
layout: post
title: "Some commands for servers with linux"
date: 2018-11-16 23:46:00 -0300
categories: tutorial linux server
---
This is a list of some utils commands for servers linux:
```bash
# Enable Global Routing on the fly
echo 1 > /proc/sys/net/ipv4/ip_forward

# Enable Global Routing permanently
# Set option: net.ipv4.ip_forward = 1
vim /etc/sysctl.conf
sysctl -p /etc/sysctl.conf

# See rules of Firewall
iptables -nL

# Avoid ICMP packages
iptables -A INPUT -p icmp --icmp-type 8 -d 192.168.1.0/24 -j DROP

# Enable forward and NAT
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -o eth1 -j ACCEPT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# Enable NTP on Firewall
iptables -A INPUT -p udp --dport 123 -j ACCEPT
iptables -A OUTPUT -p udp --sport 123 -j ACCEPT

# Query NTP Server
ntpdate -q mydomain.or.ip

```
