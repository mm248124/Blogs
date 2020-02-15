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

    #### For Debian/Ubuntu

      * wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.deb

      * sudo apt-get install ./cloudflared-stable-linux-amd64.deb
    
      * cloudflared -v

    #### For CentOS/RHEL/Fedora

      * wget https://bin.equinox.io/c/VdrWdbjqyF/cloudflared-stable-linux-amd64.rpm

      * sudo yum install ./cloudflared-stable-linux-amd64.rpm

      * cloudflared -v

