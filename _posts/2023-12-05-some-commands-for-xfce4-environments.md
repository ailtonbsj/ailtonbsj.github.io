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

# Write value to XFCE PubSub daemon (Set scale to 200%)
xfconf-query -c xsettings -p /Gdk/WindowScalingFactor -s 2

# Write value to XFCE PubSub daemon (Set theme to XFCE4 Window Manager)
xfconf-query -c xfwm4 -p /general/theme -s Default-xhdpi

# Kill PubSub deamon XFCE4
pkill xfsettingsd

# List all channels and properties of PubSub
xfce4-settings-editor
```

## References

[https://git.xfce.org/xfce/xfconf/tree/docs/spec/perchannel-xml.txt](https://git.xfce.org/xfce/xfconf/tree/docs/spec/perchannel-xml.txt)
[https://github.com/winunix/kiosk-mode-xfce4](https://github.com/winunix/kiosk-mode-xfce4)
