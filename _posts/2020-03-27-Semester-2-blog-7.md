---
layout: post
title: "Semester-2-Blog-7"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/03/27/
---

## Setup Raspberry Pi as Print Server

        A print server, or printer server, is a device that connects printers to client computers over a network. 
        
        It accepts print jobs from the computers and sends the jobs to the appropriate printers.

  __Basic setup__

        sudo su

        apt-get update && apt-get upgrade -y

        # Edit /etc/dhcpcd.conf to set static IP

        reboot

  __Server Setup__

        sudo apt-get install cups

        cupsctl --remote-any

        /etc/init.d/cups restart

  __Web Browser Access__

        # Type in your browser Raspberry pi IP and Port number

        https://RaspberryPiIP:631/

  __Add Printer__

        # Go to the Administration tab
        
            # Select Add Printer

            # Connect your printer via USB
            
            # Select printer's make and model
            
            # Enable the Share This Printer box

  __Client setup__

        # On client computer go to Printers & Scanners

            # Click Add a Printer or Scanner

            # Client computer will discover the printer

                # Click Add Printer 

            # In case client computer cannot discover printer, manually enter Raspberry Pi IP to setup your Printer