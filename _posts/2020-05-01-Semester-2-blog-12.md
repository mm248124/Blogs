---
layout: post
title: "Semester-2-Blog-12"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/05/01/
---

## Setup Webmin on Raspberry Pi

In this setup, Raspberry Pi will be a wireless access point & a router.

   __Basic setup__

        # Open terminal in Raspberry Pi
        
            sudo -i

        # Edit /etc/dhcpcd.conf to set static IP

            reboot
 
  __Update and Upgrade__

        apt-get update && apt-get upgrade -y

  __Install Webmin__

      # Install all the required packages of Webmin
      
            apt-get install perl libnet-ssleay-perl openssl libauthen-pam-perl libpam-runtime libio-pty-perl apt-show-versions python

   # Find the Latest Version at the Website

   Use this [Link](http://www.webmin.com/deb.html)
      
      # Download the files

            wget http://prdownloads.sourceforge.net/webadmin/webmin_1.941_all.deb
      
      # Use dpkg to install

            dpkg --install webmin_1.941_all.deb

  __Access Web Console__

      # After the installation web console address will be displayed

      # Access credentials will also be displayed.

      # Update Packages 
      
            Go to System > Software Package Update > Select Packages > Update Selected Packages

      # Install the Updated Packages

            Install Now

      # If you have multiple Raspberry Pis running Webmin, Create Cluster

            Go to CLuster > Cluster Webmin Servers > Select Server > Add Server

   # More Configuration Docs

   Use This [link](https://doxfer.webmin.com/Webmin/Webmin_Modules)