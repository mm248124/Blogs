---
layout: post
title: "Semester-2-Blog-1"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/02/07/
---
__Let's continue with Raspberry Pi__

### Setup Pi Hole

*I am assuming you have already installed OS on your Raspberry PI.*

Setup Static IP on your Raspberry PI.

  * sudo nano /etc/dhcpcd.conf 

  * Uncomment and set the following:

    * interface eth0
    * static ip_address=192.168.1.15    __# your IP instead__
    * static routers=192.168.1.1        __# your router IP__
  
  * Reboot Raspberry Pi

Open Terminal

  * Install curl if required

    * sudo apt-get install curl

  * Install Pi hole

    * curl -sSL https://install.pi-hole.net \| bash

  * Follow the instructions on the screen

    * Select Upstream DNS Provider

    * Go with default options or change as needed.

  __Pay attention as it will provide temp Password to access Admin Web Page__

Open Web Browser

  * "your_Pi_Hole_IP"/admin

  * Login using temp Password

Change Admin Web Page Password
  
  * Open terminal

    * sudo pihole -a -p

  Change your home router to use the static IP of your Raspberry PI as Primary DNS Server



