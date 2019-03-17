---
layout: post
title:  "Installing PHP with PostgreSQL on Ubuntu"
date:   2018-06-05 10:20:00 -0300
categories: tutorial postgresql
---
First we will install PostgreSQL and PgAdmin4:
``` 
# echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" > \
/etc/apt/sources.list.d/pgdg.list
# wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
# apt update
# apt install postgresql-10
# apt install pgadmin4
```

For see if postgre is running, use:
```bash
systemctl status postgresql
```

Connect using terminal (you have to use root) and change password:
```
# su - postgres
$ psql
postgres-# \password postgres
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
