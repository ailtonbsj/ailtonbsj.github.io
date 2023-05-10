---
layout: post
title: "Installing Intelbras SIM Next on Linux with WineHQ"
date: 2023-05-10 14:10:00 -0300
categories: tutorial linux wine
---
In this next tutorial we will learn how to install Intelbras SIM Next software on a Linux using Xubuntu 22.04 distribution.

First of all we need WineHQ Staging, so let's go to [Wine Oficial Wiki](https://wiki.winehq.org/Ubuntu) and get the commands bellow:

```bash
# Enable 32 bit architecture
sudo dpkg --add-architecture i386

# Add the public key
# Make sure the directory exist
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

# Add the source file for 22.04 (jammy)
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources

# Remove all others wine version
sudo apt remove --purge wine* fonts-wine
sudo apt autoremove

# Delete .wine folder
# THIS WILL DELETE ALL WINE APPS!
rm -rf ~/.wine

# Delete .cache folder and reboot

# Install Wine Staging
sudo apt update
sudo apt install --install-recommends winehq-staging

# Start a Wine Prefix
wineboot -u
# A Wine Mono window will prompted. Click on button Install

wine iexplore
# Open IExplorer. A Wine Gecko window will prompted. Click on button Install

# IMPORTANT: You need to change version to Windows 7
winecfg
```

You need to install Winetricks using Github script provided by [README.md Winetrick Repository](https://github.com/Winetricks/winetricks). After run the script you can do:

```bash
# Update Winetrick to last version
update_winetricks

# Install .NET 4.8
winetricks dotnet48
# Make sure to run this command with any others wine app running, or winetrick will waiting process finished!

# IMPORTANT: You need to change version to Windows 7
winecfg
```

Now we need to download the [IntelBras Sim Next](https://www.intelbras.com/pt-br/sistema-inteligente-de-monitoramento-sim-next#suporte). Extract the executable and run the command bellow:

```bash
wine SIMNext__Setup_v1.21.9_Offline.exe
```
