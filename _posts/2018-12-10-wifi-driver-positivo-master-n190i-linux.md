---
layout: post
title:  "Installing wifi driver of Positivo Master N190I Notebook on Ubuntu 18.04"
date:   2018-12-10 11:09:00 -0300
categories: tutorial linux driver
---
I have installed Lubuntu 18.04 LTS on a Positivo Master N190I Notebook, but the wifi adapter didn't work with this SO. Searching the solution I had to install a package from xenial to do the adapter work correctly.

First verify if you have a Realtek RTL8723AE using this command:
```
lspci | grep Wireless
```

Then add manually the PPA repository editing the file `/etc/apt/source.list`.
```
deb http://ppa.launchpad.net/hanipouspilot/rtlwifi/ubuntu xenial main 
# deb-src http://ppa.launchpad.net/hanipouspilot/rtlwifi/ubuntu xenial main

```

Now you have to install the packages below.
```
sudo apt update
sudo apt install rtlwifi-new-dkms linux-firmware
```

Reboot your computer and adapter will work correctly.