---
layout: post
title: "Semester-2-Blog-5"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/03/06/
---

__Setup OpenSSL__


  # Create main directory
      
      mkdir /root/ca
      
      cd /root/ca/

  # Create sub directories
      
      mkdir certs crl newcerts private request requests

  # Create File
      
      touch index.txt
      
      echo '1234' > serial

  # Generate Private Key & Certificate for CA Authority
      
      openssl genrsa -aes256 -out private/cakey.pem 4096
      
      openssl req -new -x509 -key /root/ca/private/cakey.pem  -out cacert.pem -days 3650

  # Change directory permissions 
      
      chmod 600 -R /root/ca

  # Edit openssl.cnf
  
      vi /usr/lib/ssl/openssl.cnf

        #Set root directory to /root/ca

         * Change to "dir                                     = /root/vpnCA"

  # Create Private Key & Certificate for server
      
      cd /root/ca/requests/
      
      openssl genrsa -aes256 -out webserver.pem 2048

  # Request CA Authority to sign webserver certificate
      
      openssl req -new -key webserver.pem -out webserver.csr

  # Request CA Authority to sign Certificate | webserver.csr is just cert, webserver.crt is signed cert.
      
      openssl ca -in webserver.csr -out webserver.crt

  # Copy Signed Cert to certificate directory
      
      cp webserver.crt /root/ca/certs/


  # Edit nginx to use Certificate

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

  