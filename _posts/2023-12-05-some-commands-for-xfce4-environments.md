---
layout: post
title:  "Some commands for XFCE4 environments"
date:   2023-12-05 12:00:00 -0300
categories: tutorial linux xfce4
---
This is a list of some utils command for linux environment XFCE4:
```bash
# Monitoring modifications of XFCE PubSub daemon
xfconf-query -c xfce4-desktop -m

# Read value from XFCE PubSub daemon (Get actual scale)
xfconf-query -c xsettings -p /Gdk/WindowScalingFactor
```
