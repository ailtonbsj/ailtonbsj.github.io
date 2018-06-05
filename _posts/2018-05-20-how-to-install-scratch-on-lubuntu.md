---
layout: post
title:  "How to install Scratch on Lubuntu 18.04"
date:   2018-05-20 10:20:00 -0300
categories: tutorial scratch
---
There are three ways that I know to install Scratch on the Lubuntu Linux System. The first is using Wine, the second is with Snaps' Linux and for last using online version.

Unfortunately Scratch 2 just works online, because the Adobe AIR it is no more supported by current version of linux.

## Installing Scratch 1.4 with Wine

First you need install Wine:
```
$ sudo apt update
$ sudo apt install wine64
$ wine WINEPREFIX
```

Then download the windows installer and execute it.

[http://download.scratch.mit.edu/ScratchInstaller1.4.exe](http://download.scratch.mit.edu/ScratchInstaller1.4.exe)

```
$ wine ScratchInstaller1.4.exe
```

## Instaling Scratch Berkely Snap

Using this option you will need install snapd.
```
$ sudo apt install snapd
$ sudo snap install berkeleysnap
```

Now open the browser and access the app with `http://localhost:8081`. In Chrome you can press F11 key to full screen.

## Scratch 2 online

There is also a online version of Scratch 2. Acesse in:

[https://scratch.mit.edu/projects/editor/](https://scratch.mit.edu/projects/editor/)

## Watch my tutorial on Youtube
<iframe width="100%" height="480" src="https://www.youtube.com/embed/RwoA4cDI2PU" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

If someone knows other way tell me please! Good codes for you!