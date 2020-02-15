---
layout: post
title: "Semester-2-Blog-2"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/02/14/
---
__Let's continue with Raspberry Pi__

### Configuring DNS-Over-HTTPS on Pi-hole

*With standard DNS, requests are sent in plain-text, with no method to detect tampering or misbehavior.*

*Along with releasing their DNS service 1.1.1.1, Cloudflare implemented DNS-Over-HTTPS proxy functionality into one of their tools: cloudflared.*

__Installing cloudflared__

  * Open Terminal

    ## AMD64 architecture

      ***For Debian/Ubuntu***

        * wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.deb

        * sudo apt-get install ./cloudflared-stable-linux-amd64.deb
      
        * cloudflared -v

      ***For CentOS/RHEL/Fedora***

        * wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.rpm

        * sudo yum install ./cloudflared-stable-linux-amd64.rpm

        * cloudflared -v
        
    ## ARM architecture (Raspberry Pi)

      * wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-arm.tgz

      * tar -xvzf cloudflared-stable-linux-arm.tgz

      * sudo cp ./cloudflared /usr/local/bin

      * sudo chmod +x /usr/local/bin/cloudflared

      * cloudflared -v

    ## Configure cloudflared to run on startup

      * sudo useradd -s /usr/sbin/nologin -r -M cloudflared

      ## Copy below 2 lines to the /etc/default/cloudflared file

        #Commandline args for cloudflared
        CLOUDFLARED_OPTS=--port 5053 --upstream https://1.1.1.1/dns-query --upstream https://1.0.0.1/dns-query
    
    ## Update the permissions for cloudflared

      * sudo chown cloudflared:cloudflared /etc/default/cloudflared
      * sudo chown cloudflared:cloudflared /usr/local/bin/cloudflared

    ## Copy below code to /etc/systemd/system/cloudflared.service

      [Unit]

      Description=cloudflared DNS over HTTPS proxy

      After=syslog.target network-online.target


      [Service]

      Type=simple

      User=cloudflared

      EnvironmentFile=/etc/default/cloudflared

      ExecStart=/usr/local/bin/cloudflared proxy-dns $CLOUDFLARED_OPTS

      Restart=on-failure

      RestartSec=10

      KillMode=process


      [Install]

      WantedBy=multi-user.target

    ## Enable the systemd service to run on startup, then start the service and check its status:

      * sudo systemctl enable cloudflared
      * sudo systemctl start cloudflared
      * sudo systemctl status cloudflared  

    ## Finally, configure Pi-hole to use the local cloudflared service as the upstream DNS server:

      ![DNS Settings ](https://mm248124.github.io/Blogs/assets/images/screenshots/pi_hole_dns.jpg)  

