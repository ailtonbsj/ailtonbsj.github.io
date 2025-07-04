---
layout: post
title: "Installing WhatsApp Desktop official on Linux with WineHQ"
date: 2023-05-02 00:30:00 -0300
categories: tutorial linux wine
---
In this tutorial I'll show you how to install WhatsApp Desktop official using WineHQ staging.

Let's install WineHQ Staging, all commands bellow was picked from [Wine Oficial Wiki](https://wiki.winehq.org/Ubuntu):

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

Now we need download a `WhatsAppSetup.exe` file 64 bit version from [WhatsApp website](https://www.whatsapp.com/download).

```bash
wine WhatsAppSetup.exe
```

The WhatsApp Desktop is now installed. Click on title bar e drag to top for full size of windows in Xfce4 desktop.

## Enable links from `whatsapp://`

Rename the launcher `WhatsApp (Outdated).desktop` as `WhatsApp.desktop` and open with an text editor like vim, nano or mousepad to modify with the follow parameters:

```bash
# ~/.local/share/applications/wine/Programs/WhatsApp/WhatsApp.desktop
Exec=DONT_CHANGE_THE_WINE_COMMAND_HERE_JUST_ADD_THE_FINAL_ARGUMENT.lnk %u
MimeType=x-scheme-handler/whatsapp;

# Update cache database of MIME types
update-desktop-database ~/.local/share/applications

# ALTERNATIVE: You can run xdg-mime, but you need to rename the launcher
xdg-mime default WhatsApp.desktop 'x-scheme-handler/whatsapp'
```

You can send data to WhatsApp application on browser with URIs:

```
https://wa.me/YOUR_PHONE_NUMBER?text=TEXT_URL_ENCODED

whatsapp://send/?phone=YOUR_PHONE_NUMBER&text=TEXT_URL_ENCODED

whatsapp://send?text=TEXT_URL_ENCODED
```

## Enable clicks on links (Don't works on Chrome)

You will need Firefox without snap. You can see [my video about how install](https://youtu.be/sUMBewTIJQg). 

```bash
# Open Registry Editor
wine regedit

# Go to: HKEY_CURRENT_USER\Software\Wine\WineBrowser
# Create String Value: Browsers
# Set with: firefox,xdg-open,konqueror,mozilla,netscape,galeon,opera,dillo

# Go to: HKEY_CLASSES_ROOT\http\shell\open\command
# Set Default: "C:\windows\system32\winebrowser.exe" "%1"

# Go to: HKEY_CLASSES_ROOT\https\shell\open\command
# Set Default: "C:\windows\system32\winebrowser.exe" "%1"
```

## Watch my tutorial on Youtube

<iframe width="100%" height="480" src="https://www.youtube.com/embed/tcDeD7MJ-EI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
