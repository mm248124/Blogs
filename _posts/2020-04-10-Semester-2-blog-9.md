---
layout: post
title: "Semester-2-Blog-9"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/04/10/
---

## Setup Fail2ban on the Raspberry Pi

Fail2ban is a piece of software that attempts to block malicious connections such as SSH or a web server to your device that is publicly accessible.

Fail2ban continually scans log files looking for signs of potential attacks such as too many password failures or exploits. 

It automatically updates firewall to ban IP address associated with unusual activities.
        
  __Basic setup__

        sudo su

        apt-get update && apt-get upgrade -y

        # Edit /etc/dhcpcd.conf to set static IP

        reboot

  __Update and Upgrade__

        apt-get update && sudo apt-get upgrade

  __Download and Install Fail2ban on Raspberry Pi__

        apt-get install fail2ban
        
        # fail2ban will generate a file called "jail.conf"

  __Copy "jail.conf" and name it "jail.local"__

        cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

        #Fail2ban will automatically detect and load the config

  __Edit "jail.local" file__

        vi /etc/fail2ban/jail.local

        #Search for "[sshd]" in the file and add below code under it

            enabled = true
            
            filter = sshd

  __Set Fail2ban Action__

        #Add below code to the file

        banaction = iptables-multiport

        #Additional actions can be found below location

            /etc/fail2ban/action.d/

        #Add below code to set number of attempts per user

        bantime = -1 #how long user is banned for. Value is in seconds. 1800sec = 30min. "-1" = indefinitely banned.

        maxretry = 3 #Number of tries before ban action runs.

        #Once done editing the file, save the file



  __Reboot Fail2ban service__

        service fail2ban restart

  __How to Uninstall Docker on Your Raspberry Pi__
