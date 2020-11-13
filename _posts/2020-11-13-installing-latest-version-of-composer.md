---
layout: post
title:  "Installing latest version of Composer: A Dependency Manager for PHP"
date:   2020-11-12 19:17:00 -0300
categories: tutorial composer php
---

First lets install all dependencies using APT:

```bash
sudo apt install git curl php-cli unzip
```

Now we will get de installer:

```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

Lest check if the install is corrupted:

```bash
php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

For finish we need execute the command bellow to install globally.

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```
