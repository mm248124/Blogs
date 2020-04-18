---
layout: post
title: "Semester-2-Blog-10"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/04/17/
---

## Create No IP DDNS hostname and use Raspberry Pi to update your IP

Remote access your computer, DVR, webcam, security camera or any internet connected device easily. 

Dynamic DNS points an easy to remember hostname to your dynamic IP address.
        
  __Create a hostname with No IP DDNS__

      # Go to https://www.noip.com/sign-up

            # Create and account

                  # Choose either "Free" or "Enhanced" account
            
            # Verify your email and login to noip.com

                  # Expand "Dynamic DNS" tab and select "No-IP Hostnames"

                  # Click "Create Hostname"

                        # Create a unique hostname and set your ISP IP Address
      
      # Your hostname will expire in 30 days.

            # We need to setup Dynamic Update Client (DUC) to update IP address in case it changes. This client can be run on Windows/Mac/Linux

                  # Instruction for Windows/Mac can be found under "Dynamic DNS" tab, "Dynamic Update Client"
  
  __Basic setup__

        # Open terminal in Raspberry Pi
        
        sudo -i

        # Edit /etc/dhcpcd.conf to set static IP

        reboot

  __Update and Upgrade__

        apt-get update && apt-get upgrade -y

  __Download and Install Dynamic Update Client on Raspberry Pi__

      cd /usr/local/src
      
      sudo wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz
      
      sudo tar xzf noip-duc-linux.tar.gz

      # Check version

            ls -l

      # Build the Sources
      
      cd noip-2.1.9-1

      sudo make

      sudo make install

      # Installer will prompt for few things
            
      # At the below step just say No 
            
            Do you wish to run something at successful update?[N] (y/N)

  __Run DUC as a service__

      # Create a service to run the DUC in background.

            sudo vi /etc/systemd/system/noip.service

      # Paste below code into /etc/systemd/system/noip.service file


            [Unit]
            Description=No-ip.com dynamic IP address updater
            After=network.target
            After=syslog.target

            [Install]
            WantedBy=multi-user.target
            Alias=noip.service

            [Service]
            # Start main service
            ExecStart=/usr/local/bin/noip
            Restart=always
            Type=forking

      # Enable the service to run after reboots:
      
            sudo systemctl enable noip

      # Start the service:
      
            sudo systemctl start noip

      # Additionally you can see the status of the service by typing:
      
            sudo service noip status