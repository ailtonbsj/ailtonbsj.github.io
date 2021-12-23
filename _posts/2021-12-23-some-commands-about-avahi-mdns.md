---
layout: post
title: "Some commands about Avahi mDNS/DNS-SD"
date: 2021-12-22 08:40:00 -0300
categories: tutorial linux mdns
---
Bonjour Zeroconf architecture created by Apple was implemented as an open-source project called Avahi. This is some commands utils to get information on your network. Check for packages `avahi*` for more details.

```bash
# Browse for mDNS/DNS-SD services using the Avahi daemon
apt install avahi-discover

# Scan to discover local services
avahi-browse --all --ignore-local --resolve --terminate

# Scan and strutured output
avahi-browse -tpkar -l | grep 'enp2s0;IPv4' | less

# Scan and better strutured output
avahi-browse -tpkarl | grep '=;enp2s0;IPv4;' | cut -d';' -f5-

# Resolve FQDN to IP
avahi-resolve -n adm1.local
getent hosts adm1.local

# Resolve IP to name
avahi-resolve -a 192.168.1.7

# Publish IP Address for resolution with avahi-resolve
avahi-publish-address adm1.local 172.18.0.3
avahi-publish-address -R adm1.local 192.168.1.7

# Publish service for discovery with avahi-browse
avahi-publish-service "MyApacheService" _http._tcp 8080
avahi-publish-service "MyAdminerService" _http._tcp 8081 "db=scholarevents"
avahi-publish-service -H adm1.local "AdminerService" _http._tcp 8080 "db=scholarevents"

# Collect traffic from mdns (dns-sd) protocol
sudo tcpdump -n -s0 port 5353

# Some types of service
_device-info._tcp
_smb._tcp
_ftp._tcp
_http._tcp
_uscans._tcp
_uscan._tcp
_scanner._tcp
_privet._tcp
_printer._tcp
_ipps._tcp
_ipp._tcp
_pdl-datastream._tcp
```