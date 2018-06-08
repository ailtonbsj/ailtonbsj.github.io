---
layout: post
title:  "Creating a launcher for XAMPP on Lubuntu 18.04"
date:   2018-06-08 10:30:00 -0300
categories: tutorial xampp
---
The script installer of XAMPP don't create a default launcher for the application, being necessary start services of apache, mysql or proftpd by terminal.

We can start the services with this commands:

```
$ sudo /opt/lampp/lampp startapache
$ sudo /opt/lampp/lampp startmysql
$ sudo /opt/lampp/lampp startftp
```

For to turnoff the services we using this:

```
$ sudo /opt/lampp/lampp stopapache
$ sudo /opt/lampp/lampp stopmysql
$ sudo /opt/lampp/lampp stopftp
```

Lets then create a launcher to turn this task easy using a control panel. Save this code, change permissions to execute them:

<script src="https://gist.github.com/ailtonbsj/539f9a39e829c2bab730ff1eca6a06d3.js"></script>