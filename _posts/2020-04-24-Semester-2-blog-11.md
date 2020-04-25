---
layout: post
title: "Semester-2-Blog-11"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/04/17/
---

## Setup Raspberry Pi as a Wireless access point & Router

In this setup, Raspberry Pi will be a wireless access point & a router.

  __Update and Upgrade__

        apt-get update && apt-get upgrade -y

  __Install hostapd & dnsmasq__

      sudo apt-get install hostapd dnsmasq -y
      
  __Stop hostapd & dnsmasq Services__

     systemctl stop hostapd dnsmasq

  __Set a static IP for the wlan0 interface__

      # Edit file /etc/dhcpcd.conf

            vi /etc/dhcpcd.conf

            # Add below code at the end of the file

                  interface wlan0

                  static ip_address=192.168.2.1/24

                  denyinterfaces eth0

                  denyinterfaces wlan0

  __Configure the DHCP Server dnsmasq__

      # Rename default config file

            mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig

      # Create new config file

            vi /etc/dnsmasq.conf

                  # Copy below code to the file

                        interface=wlan0
                        
                        dhcp-range=192.168.2.100,192.168.2.199,255.255.255.0,24h

  __Configure the Access Point Software (hostapd)__

      # Edit hostapd config file

            vi /etc/hostapd/hostapd.conf

            # Copy below code to the file & change "NETWORK" & "PASSWORD"

                  interface=wlan0

                  bridge=br0

                  hw_mode=g

                  channel=7

                  wmm_enabled=0

                  macaddr_acl=0

                  auth_algs=1

                  ignore_broadcast_ssid=0

                  wpa=2

                  wpa_key_mgmt=WPA-PSK

                  wpa_pairwise=TKIP

                  rsn_pairwise=CCMP

                  # WiFi Name
                  ssid=NETWORK

                  # WiFi Password
                  wpa_passphrase=PASSWORD

            # Edit config file to 
  
                  vi /etc/default/hostapd

                  # Add below code to the file

                        DAEMON_CONF="/etc/hostapd/hostapd.conf"

  __Set Up Forwarding__

      # Raspberry Pi will forward the traffic from wlan0 through Ethernet Port to Modem.

      # Edit file

            vi /etc/sysctl.conf

            # Locate "#net.ipv4.ip_forward=1" and uncomment it (delete "#")

   __Setup iptables rule__
      
      # add IP masquerading for outbound traffic on eth0 
      
            iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

      # Save New iptables Rule

            sh -c "iptables-save > /etc/iptables.ipv4.nat"

      # Edit the file /etc/rc.local to Load the Rule on Boot

            vi /etc/rc.local

                  # Add below code to the file just above the line "exit 0"

                        iptables-restore < /etc/iptables.ipv4.nat

  __Setup Internet Connection__
      
      # Build bridge to pass all traffic between the wlan0 and eth0 interfaces

            apt-get install bridge-utils

      # Add a new bridge called br0

            brctl addbr br0

      # Connect eth0 interface to bridge

            brctl addif br0 eth0

      # Edit the interfaces file

            vi /etc/network/interfaces

            # Add below code to the end of the file

                  auto br0

                  iface br0 inet manual

                  bridge_ports eth0 wlan0

      # Reboot

            reboot


















































