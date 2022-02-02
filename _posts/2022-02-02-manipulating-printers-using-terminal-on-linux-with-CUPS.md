---
layout: post
title: "Manipulating printers using terminal on Linux with CUPS"
date: 2022-02-02 08:27:00 -0300
categories: tutorial linux cups
---
In this article I'll show how to manipulate printers on a linux desktop use some commands available on the `cups` package.

First of all, we need install the package cups on our machine. Use the follow command on debian and derivatives:

```bash
sudo apt install cups
```

Here are some commands to manipulate printers:

```bash
# List all models
lpinfo -m

# List all backends class available
lpinfo -v

# Add Network Printer using everywhere driver
lpadmin -p MyPrinter -E -v ipp://11.22.33.44/ipp/print -m everywhere -o PageSize=A4 -o printer-is-shared=false -u allow:all

# Add Network Printer using legacy driver
lpadmin -p printername -E -v socket://11.22.33.44 -m drv:///sample.drv/laserjet.ppd -o PageSize=A4 -o printer-is-shared=false -u allow:all

# URI (Backends) types
- dnssd: The Bonjour (DNS-SD) protocol.
- ipp: The Internet Printing Protocol (IPP) with optional encryption.
- ipps: The Internet Printing Protocol with mandatory encryption.
- lpd: The Line Printer Daemon protocol.
- socket: The AppSocket (JetDirect) protocol.
- usb: The Universal Serial Bus (USB) printer class.

# Delete a printer
lpadmin -x printername

# Enable share printers
cupsctl --share-printers
```