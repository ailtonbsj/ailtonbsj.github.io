---
layout: post
title:  "Some utils commands to monitoring and logging user and system"
date:   2019-03-16 21:54:00 -0300
categories: tutorial linux hacker
---
This is a list of some utils:
```bash
# Tell how long the system has been running
uptime -s
uptime -p

# Show who is logged on and what they are doing
w
w -h
who -a
who -u
users

# Show a listing of last logged in users
last
sudo lastb
last -a -d

# Display the system shutdown entries and run level changes
last -x
last reboot
last reboot -a
last -x | grep shutdown
last -x | grep reboot

# Logs
cat /var/log/syslog
cat /var/log/kern.log
cat /var/log/boot.log

# List all services
service --status-all
systemctl list-units --type service

# Status and Log of service
systemctl status service-name
journalctl -u service-name

```
