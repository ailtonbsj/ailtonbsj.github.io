---
layout: post
title: "Installing Java JDK 17 LTS on debian distros"
date: 2021-11-13 14:00:00 -0300
categories: tutorial linux java
---
This tutorial we will learn how to install JDK on linux systems based on debian.

## Java 17 LTS Global

```bash
# Download JDK on Oracle Website
apt install ./jdk-17.deb

# Manage bins with update-alternatives
update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-17/bin/java 100
update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-17/bin/javac 100
update-alternatives --install /usr/bin/jar jar /usr/lib/jvm/jdk-17/bin/jar 100

# Add JAVA_HOME to PATH
vim /etc/profile.d/java17.sh
## export JAVA_HOME=/usr/lib/jvm/jdk-17
## export PATH=$PATH:$JAVA_HOME/bin
```

## OpenJDK 11 LTS Global

```bash
# Install JDK 11 LTS
apt install openjdk-11-jdk

# Manage bin with update-alternatives
update-alternatives --config java

vim /etc/profile.d/jdk-11.sh
## export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```