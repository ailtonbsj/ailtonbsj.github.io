---
layout: post
title:  "Running Windows Apps on Lubuntu 20.04 with Wine"
date:   2019-10-20 14:44:00 -0300
categories: tutorial linux windows
---
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
sudo apt install fonts-wine
```

Now we will to create a Wine Prefix.

```bash
wine start hostname
```

We can start a windows app, access the wine settings and control panel with those commands bellow.

```bash
wine start control
wine start notepad.exe
winecfg
```
We need to download some MSI packages of [Mono](https://wiki.winehq.org/Mono) and [Gecko](https://wiki.winehq.org/Gecko) to improve wine.

- [wine-mono-x86.msi](https://dl.winehq.org/wine/wine-mono/5.1.0/wine-mono-5.1.0-x86.msi)
- [wine_gecko-x86.msi](http://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86.msi)
- [wine_gecko-x86_64.msi](http://dl.winehq.org/wine/wine-gecko/2.47.1/wine-gecko-2.47.1-x86_64.msi)

Let's install the packages on wine.

```bash
wine msiexec /i ./wine-mono-5.1.0-x86.msi
wine msiexec /i ./wine-gecko-2.47.1-x86_64.msi
wine msiexec /i ./wine-gecko-2.47.1-x86.msi
```

We need install some extra packages like .NET and Visual C++.

```bash
winetricks dotnet46
winetricks vcrun2012
```

Another utils commands are:
```bash
wine --version
winetricks list
winetricks apps list
```
