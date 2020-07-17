---
layout: post
title:  "How to install Packet Tracer 7.3 on Ubuntu 20.04 LTS in mode noninteractive"
date:   2020-07-12 16:20:00 -0300
categories: tutorial linux debian
---

First of all, if you don't use WinuniX OS, you need add the Winunix repository. Follow the steps in:

[https://winunix.github.io/debian](https://winunix.github.io/debian)

Now run the commands on terminal to install Packet Tracer 7.3 in mode noninteractive:

```bash
echo debconf PacketTracer_730_amd64/accept-eula select true | sudo debconf-set-selections

echo debconf PacketTracer_730_amd64/show-eula select false | sudo debconf-set-selections
```

You need go on [https://www.netacad.com](https://www.netacad.com) and download the `deb` package then run the command:

```bash
sudo DEBIAN_FRONTEND=noninteractive apt install ./PacketTracer_*.deb
```
