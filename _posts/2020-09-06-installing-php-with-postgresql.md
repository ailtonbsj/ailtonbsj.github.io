---
layout: post
title:  "Installing PHP with PostgreSQL on Ubuntu"
date:   2020-09-06 23:09:00 -0300
categories: tutorial postgresql php
---
First we will install PostgreSQL and PgAdmin4:

```bash
# Add keys of repository
curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add

# Add repository
echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" | sudo tee /etc/apt/sources.list.d/pgadmin4.list

# Update list of packages
sudo apt update

# Install both desktop and web modes apps
sudo apt install pgadmin4

# Configure the webserver, if you installed pgadmin4-web:
sudo /usr/pgadmin4/bin/setup-web.sh
```

Now you can use PgAdmin4 to connect the database!

Lets install PHP and dependencies to access the database:

```bash
$ sudo apt install php
$ sudo apt install php-pgsql
$ sudo apt install php-xml
$ sudo apt install php-zip
$ sudo apt install php-mbstring
```

You can run the embed webserver with:
```bash
php -S localhost:8000
```
