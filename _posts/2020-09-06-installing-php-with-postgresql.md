---
layout: post
title:  "Installing PHP with PostgreSQL on Ubuntu"
date:   2020-09-06 23:09:00 -0300
categories: tutorial postgresql php
---
First we will add the official Postgre repository:

```bash
# Add keys of repository
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Add repository
echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list

# Update list of packages
sudo apt update
```

Now we will install Postgree:

```bash
sudo apt install postgresql
```

For fininish lets install pgAdmin:

```bash
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
