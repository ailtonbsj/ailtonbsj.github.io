---
layout: post
title:  "Running Windows Apps on Lubuntu 20.04 with Wine"
date:   2019-10-20 14:44:00 -0300
categories: tutorial linux windows
---

## Installing Wine

Let's start applying a i386 architecture in our x64 system.

```bash
sudo dpkg --add-architecture i386
sudo apt update
```

Now let's installing the necessaries packages of wine.

```bash
sudo apt install --install-recommends wine64
sudo apt install --install-recommends winetricks
sudo apt install --install-recommends wine-binfmt
sudo apt install --install-recommends winbind
sudo apt install --install-recommends mono-complete
sudo apt install cabextract
sudo apt install fonts-wine
```

Now we will to create a Wine Prefix.

```bash
wineboot -u
# Alternative: wine start hostname
```

We need to download some MSI packages of [Mono](https://wiki.winehq.org/Mono) and [Gecko](https://wiki.winehq.org/Gecko) to improve wine.

Let's install the packages on wine.

```bash
# Mono
wget https://dl.winehq.org/wine/wine-mono/5.1.0/wine-mono-5.1.0-x86.msi
wine msiexec /i ./wine-mono-5.1.0-x86.msi

# Gecko 32 bits
wget http://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86.msi
wine msiexec /i ./wine-gecko-2.47.1-x86.msi

# Gecko 64 bits (need 32)
wget http://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86_64.msi
wine msiexec /i ./wine-gecko-2.47.1-x86_64.msi
```

## Some tricks

We can start a windows app, access the wine settings and control panel with those commands bellow.

```bash
# Change Windows version, set libraries and drive
winecfg

# Control Panel
wine start control

# To run some app in Prefix path
wine start notepad.exe

# To run some app out of Prefix path
wine start /unix /usr/share/sample/app.exe
```

We may need install some extra packages like .NET and Visual C++.

```bash
# .NET 3.5
winetricks dotnet35

# .NET 4.6
winetricks dotnet46

# Visual C++ libraris 2012
winetricks vcrun2012

# Extra fonts
winetricks tahoma corefonts ie8

...
```

Another utils commands are:
```bash
wine --version
winetricks list
winetricks list-all
winetricks apps list
```
