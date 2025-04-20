---
layout: post
title: "Installing Oracle Forms 10g on Linux with WineHQ"
date: 2025-04-20 19:00:00 -0300
categories: tutorial linux wine
---
Welcome to the tutorial of how to install Oracle Forms and Reports 10g on Ubuntu 24.04 LTS distribution.

The next steps will install WineHQ, you can check this informations on [Wine Oficial Wiki](https://gitlab.winehq.org/wine/wine/-/wikis/Debian-Ubuntu).

```bash
# Delete .wine folder
# THIS WILL DELETE ALL WINE APPS!
rm -rf ~/.wine
rm -rf ~/.local/share/applications/wine

# Remove all others wine version
sudo apt remove --purge wine* fonts-wine
sudo apt autoremove

# Delete .cache folder and reboot

# Enable 32 bit architecture
sudo dpkg --add-architecture i386

# Add the public key
# Make sure the directory exist
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

# Add the source file for 24.04 (noble)
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources

# Install WineHQ
sudo apt update
sudo apt install --install-recommends winehq-stable

# Start a Wine Prefix
# A Wine Mono window will prompted. Click on button Install
wineboot -u

# Open IExplorer. A Wine Gecko window will prompted. Click on button Install
wine iexplore

# IMPORTANT: You need to change version to Windows XP
winecfg

# Copy file MemoryManagement.reg to ~/.wine/drive_c/
# Import reg file with regedit
cd ~/.wine/drive_c/
wine regedit

# Copy installer folder Oracle_Developer_Suite_10g with Disk1 and Disk2 to ~/.wine/drive_c/
cd ~/.wine/drive_c/Oracle_Developer_Suite_10g/Disk1/
wine setup.exe

# Follow: Next > Next > Next > (*) Complete > Next > Next > Install > Exit > Yes
# Reboot your system
```

### Content of file `MemoryManagement.reg`

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"ClearPageFileAtShutdown"=dword:00000000
"DisablePagingExecutive"=dword:00000000
"LargeSystemCache"=dword:00000000
"NonPagedPoolQuota"=dword:00000000
"NonPagedPoolSize"=dword:00000000
"PagedPoolQuota"=dword:00000000
"PagedPoolSize"=dword:00000000
"SecondLevelDataCache"=dword:00000000
"SessionPoolSize"=dword:00000004
"SessionViewSize"=dword:00000030
"SystemPages"=dword:00000000
"PagingFiles"=hex(7):63,00,3a,00,5c,00,70,00,61,00,67,00,65,00,66,00,69,00,6c,\
  00,65,00,2e,00,73,00,79,00,73,00,20,00,31,00,35,00,33,00,35,00,20,00,31,00,\
  35,00,33,00,35,00,00,00,00,00
"PhysicalAddressExtension"=dword:00000001
"ExistingPageFiles"=hex(7):5c,00,3f,00,3f,00,5c,00,43,00,3a,00,5c,00,70,00,61,\
  00,67,00,65,00,66,00,69,00,6c,00,65,00,2e,00,73,00,79,00,73,00,00,00,00,00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters]
"BootId"=dword:00000023
"BaseTime"=dword:2ca33473
"EnableSuperfetch"=dword:00000003
"EnablePrefetcher"=dword:00000003
"EnableBootTrace"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\StoreParameters]
```
