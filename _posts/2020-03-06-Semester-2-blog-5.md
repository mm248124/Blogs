---
layout: post
title: "Semester-2-Blog-5"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/03/06/
---

## Setup OpenSSL


  __Create main directory__
      
      mkdir /root/ca
      
      cd /root/ca/

  __Create sub directories__
      
      mkdir certs crl newcerts private request requests

  __Create File__
      
      touch index.txt
      
      echo '1234' > serial

  __Generate Private Key & Certificate for CA Authority__
      
      openssl genrsa -aes256 -out private/cakey.pem 4096
      
      openssl req -new -x509 -key /root/ca/private/cakey.pem  -out cacert.pem -days 3650

  __Change directory permissions__
      
      chmod 600 -R /root/ca

  __Edit openssl.cnf__

      vi /usr/lib/ssl/openssl.cnf

        #Set root directory to /root/ca

         * Change to "dir                                     = /root/vpnCA"

  __Create Private Key & Certificate for server__
      
      cd /root/ca/requests/
      
      openssl genrsa -aes256 -out webserver.pem 2048

  __Request CA Authority to sign webserver certificate__
      
      openssl req -new -key webserver.pem -out webserver.csr

  __Request CA Authority to sign Certificate \| webserver.csr is just cert, webserver.crt is signed cert__
      
      openssl ca -in webserver.csr -out webserver.crt

  __Copy Signed Cert to certificate directory__
      
      cp webserver.crt /root/ca/certs/


  __Edit nginx to use Certificate__

    # /etc/nginx/sites-available/default

    server {

            listen 443 default_server;

            listen [::]:443 default_server;
            
            root /var/www/html;
            
            index index.html index.htm index.nginx-debian.html;

            server_name _;

            location / {

                    # First attempt to serve request as file, then

                    # as directory, then fall back to displaying a 404.

                    try_files $uri $uri/ =404;
            }

            ssl on;

            ssl_certificate /etc/nginx/certs/webserver.crt;

            ssl_certificate_key /etc/nginx/certs/webserver.key;

            # If your Private key has password then provide password in the file
            
              ssl_password_file /etc/nginx/certs/password.pass;

    }

  