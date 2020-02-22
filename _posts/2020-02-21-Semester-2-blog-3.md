---
layout: post
title: "Semester-2-Blog-3"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/02/21/
---
__Raspberry Pi VPN__

### Setup an OpenVPN Server

*VPN stands for Virtual Private Network, a secure network that is not restricted to one geographical location.*

*A Virtual Private Network provides you with two major features: Encryption & Authentication*

__Installing OpenVPN_

  * Open Terminal

    * sudo apt-get update

    * sudo apt-get upgrade
    
    * curl -L https://install.pivpn.io \| bash

    * Follow the prompt

    * Set Static IP when Prompted

    * Set Default Gateway

    * Choose a user

    * Choose TCP or UDP (recommended)

    * Choose Port number

    * Select DNS Provider

    * Finish setup

    * Reboot

   __Setup your Client__

  * Open Terminal

    * sudo apt-get update

    * pivpn add

    * Provide username

  __Port Forwarding__

    * Enable Port forwarding on your Router to IP and Port that you configured.

  __Connecting to the VPN__

    * Install OpenVPN Client on your device

    * Copy generated file to the device.

    * Use the config to connect to VPN

   


