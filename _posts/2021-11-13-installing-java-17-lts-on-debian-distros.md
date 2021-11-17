---
layout: post
title: "Installing Java JDK 17 LTS on debian distros"
date: 2021-11-13 14:00:00 -0300
categories: tutorial linux java
---
This tutorial we will learn how to install JDK on linux systems based on debian.

## Java 17 LTS

```bash
# Download JDK on Oracle Website
sudo apt install ./jdk-17.deb

# Add JAVA_HOME to PATH
sudo vim /etc/profile.d/java17.sh
## export JAVA_HOME=/usr/lib/jvm/jdk-17
## export PATH=$PATH:$JAVA_HOME/bin

update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.12/bin/java 100
```

## OpenJDK 11 LTS Global

```bash
# Install JDK 11 LTS
sudo apt install openjdk-11-jdk

sudo vim /etc/profile.d/jdk-11.sh
## export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

sudo update-alternatives --config java
```