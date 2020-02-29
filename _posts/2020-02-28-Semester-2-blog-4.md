---
layout: post
title: "Semester-2-Blog-4"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/02/28/
---

### Setup nginx


__Update OS__

  * apt-get update

  * apt-get upgrade

__Install nginx__

  * apt-get install nginx

__Start nginx__

  * sudo /etc/init.d/nginx start

__Test nginx__

    * Point your web browser at your domain name or IP address

###  nginx makes it very simple to create virtual hosts, allowing you to host multiple websites on a single (ve) Server. 

  __Make directories for websites__

    * cd /var/www/

    * mkdir -p /var/www/ve-server{1,2}.com/{public,logs}

  __Copy And Paste into /var/www/ve-server1.com/public/index.html__

    <html>

      <head>

        <title>Welcome to nginx!</title>

      </head>

      <body bgcolor="white" text="black">

        <center><h1>ve-server1.com is working!</h1></center>

      </body>

    </html>

  __Copy And Paste into /var/www/ve-server2.com/public/index.html__

    <html>
      
      <head>
          
        <title>Welcome to nginx!</title>\n</head>
          
        <body bgcolor="white" text="black">
        
          <center><h1>ve-server2.com is working!</h1></center>
          
        </body>
        
    </html>

  __Create /etc/nginx/sites-available/ve-server1.com file__

      * vi /etc/nginx/sites-available/ve-server1.com

  __Copy the following into /etc/nginx/sites-available/ve-server1.com__

      server {

      listen   80;

      server_name  www.ve-server1.com;

      rewrite ^/(.*) http://ve-server1.com/$1 permanent;

      }

      server {

      listen   80;

      server_name ve-server1.com;

      access_log /var/www/ve-server1.com/logs/access.log;

      error_log /var/www/ve-server1.com/logs/error.log;

      location / {

      root   /var/www/ve-server1.com/public/;

      index  index.html;

      }

      }

  __Create /etc/nginx/sites-available/ve-server2.com file__

    * vi /etc/nginx/sites-available/ve-server2.com

      server {

      listen   80;

      server_name  www.ve-server2.com;

      rewrite ^/(.*) http://ve-server2.com/$1 permanent;

      }

      server {

      listen   80;

      server_name ve-server2.com;

      access_log /var/www/ve-server2.com/logs/access.log;

      error_log /var/www/ve-server2.com/logs/error.log;

      location / {

      root   /var/www/ve-server2.com/public/;

      index  index.html;

      }

      }

  __create symbolic links for the files we just created__

    * ln -s /etc/nginx/sites-available/ve-server1.com /etc/nginx/sites-enabled/ve-server1.com

    * ln -s /etc/nginx/sites-available/ve-server2.com /etc/nginx/sites-enabled/ve-server2.com

  __Restart nginx__

    * /etc/init.d/nginx restart
   


