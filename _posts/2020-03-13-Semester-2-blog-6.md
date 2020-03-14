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

    OpenMediaVault is the next generation network attached storage (NAS) solution based on Debian Linux.

    It contains services like SSH, (S)FTP, SMB/CIFS, DAAP media server, RSync, BitTorrent client and many more. 
    
    Thanks to the modular design of the framework it can be enhanced via plugins.

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

        #Change Auto logout to Disabled.

            Go to *General Settings* > "Web Administration"
            
                change *Session timeout* to 0

                    Click *Save* > *Apply*
    
        #Change the Web Administrative Password to a strong password.

            Go to *General Settings* > *Web Administrator Password*

                Type in new Password

                Click *Save* > *Apply*

        #add a Ethernet interface.

            Go to *Network* > *Interfaces*

                *Add* > *Ethernet* 

                    Select your device interface

                    For IPv4 select *DHCP*

                    Click *Save* > *Apply*

        #Updates

            Go to *Update Management*

                Select All packages 

                    Upgrade/Install

        #Format Disk

            Connect your USB hard drive to Raspberry Pi

            Go to *Disks*

                Click Scan

                Once Scan finds your disk, select that disk then click *Wipe*

        #Create and attach Volume

            Go to *File System*

                Click *Create*

                    Select the scanned drive
                    
                    Type in label (e.g. data)

                    Click *OK* (It will take a while)

                Select the created device

                    Click *Mount*

                        Click *Apply*

        #Create user

            Go to *User*

                Add user

        #Create Shared folder

            Go to *Shared Folders*

                Click *Add*

                    Provide the following:

                        Name:

                        Device:

                        Path:

                        Permissions:

                    Click *Save*

        #Create Share

            Go to *SMB/CIFS* > *Shares*

                Click *Add*

                    Fill out the info

                        Click *Save*

            Go to *SMB/CIFS* > *Settings*

                Enable

                Click *Save*