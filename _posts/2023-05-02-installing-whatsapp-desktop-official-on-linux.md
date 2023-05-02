---
layout: post
title: "Installing WhatsApp Desktop official on Linux"
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
sudo apt remove --purge wine*
sudo apt autoremove

# Install Wine Staging
sudo apt update
sudo apt install --install-recommends winehq-staging

# Start a Wine Prefix
wineboot -u
# A Wine Mono window will prompted. Click on button Install
```

You need to install Winetricks using Github script provided by [README.md Winetrick Repository](https://github.com/Winetricks/winetricks). After run the script you can do:

```bash
# Update Winetrick to last version
update_winetricks

# Install .NET 4.5
winetricks dotnet45
# Make sure to run this command with any others wine app running, or winetrick will waiting process finished!

# IMPORTANT: You need to change version to Windows 7
winecfg
```

Now we need download a `WhatsAppSetup.exe` file 64 bit version from [WhatsApp website](https://www.whatsapp.com/download).

```bash
wine WhatsAppSetup.exe
```

The WhatsApp Desktop is now installed. Click on title bar e drag to top for full size of windows in Xfce4 desktop.

## Enable links from `whatsapp://`

Open the launcher `WhatsApp (Outdated).desktop` with an text editor like vim, nano or mousepad and add the line bellow on end:

```bash
# ~/.local/share/applications/wine/Programs/WhatsApp/WhatsApp (Outdated).desktop`
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
