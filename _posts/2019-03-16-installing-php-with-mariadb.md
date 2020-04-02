---
layout: post
title:  "Installing PHP with MariaDB on Ubuntu"
date:   2019-03-16 21:45:00 -0300
categories: tutorial linux web
---
This is a tutorial to install Php, MariaDB and PhpMyAdmin on Bionic Beaver:
```bash
# Installing apache web server
sudo apt install apache2
sudo systemctl status apache2

# Installing MariaDB
sudo apt install mariadb-server mariadb-client
sudo systemctl status mysql
sudo mysql_secure_installation
# Ask to root password (enter for none)
# Y for all questions

# Installing PHP
sudo apt install php
sudo apt install php-common     
sudo apt install php-mysql
sudo apt install php-gd
sudo apt install php-cli
sudo apt install php-mbstring
sudo apt install php-gettext

# Creating PHP Info
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
# http://localhost/info.php

# Installing phpMyAdmin
sudo apt install phpmyadmin
# You need select option: apache2
# Set a password for user 'phpmyadmin'
sudo systemctl restart apache2

# Enable conf of apache if don't exist
sudo cp /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin
sudo systemctl restart apache2

# Enabling super access on phpmyadmin
sudo mysql -u root -p
# Execute the follow queries
# CREATE USER 'admin'@'localhost' IDENTIFIED BY '123';
# GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
# FLUSH PRIVILEGES;
```

## Fix bug on phpMyAdmin

On terminal type this:
```bash
sudo nano +613 /usr/share/phpmyadmin/libraries/sql.lib.php
```

Replace this code:
```php
((empty($analyzed_sql_results['select_expr']))
    || (count($analyzed_sql_results['select_expr'] == 1)
        && ($analyzed_sql_results['select_expr'][0] == '*')))
```

With this code:
```php
((empty($analyzed_sql_results['select_expr']))
    || (count($analyzed_sql_results['select_expr']) == 1)
        && ($analyzed_sql_results['select_expr'][0] == '*'))
```

You have to restart apache:
```bash
sudo systemctl restart apache2
```

Now you can use phpMyAdmin with user `admin` and password `123`.

### References

https://www.tecmint.com/install-lamp-with-phpmyadmin-in-ubuntu-18-04/

https://stackoverflow.com/questions/48001569/phpmyadmin-count-parameter-must-be-an-array-or-an-object-that-implements-co