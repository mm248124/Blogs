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

  Uncomment and set the following:

    * interface eth0
    * static ip_address=192.168.1.15    # your IP instead
    * static routers=192.168.1.1        # your router IP

    







You can buy a Raspberry Pi 4 full kit from Amazon.com for $80-$100

After you buy your Raspberry Pi you need to install OS on the SD Card.

  * You can download it from [Raspberry Pi](https://www.raspberrypi.org/downloads/)

Choose between Noobs, Raspbian or third party OS like (Ubuntu MATE, Ubuntu Core, Ubuntu Server, Windows 10 IoT Core ...)

If you choose *Noobs*, you get the following 2 choices:

    * NOOBS Lite
  
    * NOOBS

If you choose *Raspbian*, you get the following 3 choices:

    * Raspbian Buster Lite

    * Raspbian Buster with desktop

    * Raspbian Buster with desktop and recommended software

Choose your download method:

    * ZIP

    * Torrent

To install OS on the SD Card we need a software called *balenaEtcher*

 * You can download it from [balenaEtcher](https://www.balena.io/etcher/)

* Install *balenaEtcher*

Steps to install OS:

    * Run *balenaEtcher*

    * Select Image that you downloaded earlier

    * Select Target as your SD Card

    * Click Flash

Once done, insert it in Raspberry Pi & power on the device.

Click the link below to view possible projects to do with your new Raspberry Pi.

  * [Raspberry Pi Projects](https://pimylifeup.com/category/projects/)


