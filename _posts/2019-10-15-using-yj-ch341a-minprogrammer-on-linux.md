---
layout: post
title:  "Using YJ CH341A Mini Programmer on Linux"
date:   2019-10-15 11:59:00 -0300
categories: tutorial linux hardware
---
This tutorial describes some commands to read and write flash chips using the device CH341A.

```bash
# Download the programmer app
sudo apt update
sudo apt install flashrom

# Do the backup of old bios
sudo flashrom -p ch341a_spi -r bkp.bin

# Write the binary of new bios
sudo flashrom -p ch341a_spi -w bios.bin

# Read the writed bios
sudo flashrom -p ch341a_spi -r writed.bin

# Check if is writed with success
diff -sq writed.bin bios.bin
```
