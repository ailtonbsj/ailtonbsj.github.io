---
layout: post
title:  "Running Windows Apps on linux with Wine"
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
We need to download some MSI packages of mono and gecko to improve wine.

- [wine-mono-4.9.4.msi](http://dl.winehq.org/wine/wine-mono/4.9.4/wine-mono-4.9.4.msi)
- [wine_gecko-2.47-x86.msi](http://dl.winehq.org/wine/wine-gecko/2.47/wine_gecko-2.47-x86.msi)
- [wine_gecko-2.47-x86_64.msi](http://dl.winehq.org/wine/wine-gecko/2.47/wine_gecko-2.47-x86_64.msi)

Let's install the packages on wine.

```bash
wine msiexec /i wine-mono-4.9.3.msi
wine msiexec /i wine_gecko-2.47-x86_64.msi
wine msiexec /i wine_gecko-2.47-x86.msi
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
