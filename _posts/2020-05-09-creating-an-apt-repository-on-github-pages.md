---
layout: post
title:  "Creating an APT repository on Github pages"
date:   2020-05-09 15:04:00 -0300
categories: tutorial linux debian github
---
You can host debian packages on Github and provide these files for the APT package manager to download from the terminal.

Initially do:
```bash
sudo apt-get install reprepro

mkdir -p myrepo/{conf,incoming}
cd myrepo

cat <<EOF >> conf/distributions
Origin: NameOfProvider
Label: LabelOfProvider
Suite: stable
Codename: focal
Architectures: i386 amd64
Components: main
Description: Debian x86-64 packages hosted on githubpages
SignWith: MY-KEY-TO-SIGN-THE-PACKAGES
EOF

cp ../../public.key .
```

To include new deb packages use:
```bash
reprepro includedeb focal ../my_deb_package.deb
```

To list all packages in your repository:
```bash
reprepro list focal
```

To Remove package:
```bash
reprepro remove focal PACKAGE
```


After upload the folder to github pages, you can add the repository:
```bash
wget -qO - 'https://winunix.github.io/debian/public.key' | sudo apt-key add -
sudo add-apt-repository 'deb https://winunix.github.io/debian focal main'

# Host locally with PHP
# deb http://0.0.0.0:8080/debian focal main
# http://0.0.0.0:8080/public.key
```