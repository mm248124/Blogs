---
layout: post
title: "Semester-2-Blog-6"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/03/13/
---

## Setup OpenMediaVault on Raspberry Pi


  __Update Raspberry Pi__

        sudo su

        apt-get update && apt-get upgrade -y

        reboot

  __Run given command to download the OpenMediaVault__

        wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash

        #If the Script gets stuck, type IP address of Raspberry Pi in a Web Browser. If OpenMediaVault comes up, type q to exit the script.

  __Reboot Raspberry Pi__

        reboot

  __Log into OMV (OpenMediaVault)__

    Type Raspberry Pi IP in Web Browser

        Default Username : admin
        Default Password : openmediavault

  __Configure OpenMediaVault__
        #Firstly, you need to change Auto logout to Disabled.
            Go to *General Settings* > 
                *Web Administration* > change *Session timeout* to 0
                    Click *Save* > *Apply*
                *Web Administrator Password*
                    Type in new Password
            



Secondly, change the Web Administrative Password to a strong password of your choice.

Thirdly, navigate to system > Network and add a Ethernet interface.
Under General settings, we need to select our eth0 Ethernet Interface.
After that under IPv4, we need to select DHCP and save the configuration.
