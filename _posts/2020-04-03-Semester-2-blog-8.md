---
layout: post
title: "Semester-2-Blog-8"
description: "CIT 481 Second blog"
categories: [uncategorized]
tags: [random, jekyll]
redirect_from:
  - /2020/04/03/
---

## Setup Docker on Raspberry Pi

        Docker is a tool for creating, deploying, and running applications in containers. 

        Docker containers are lightweight, especially compared to virtual machines. This feature is especially valuable if you are a Raspberry Pi user.
  __Basic setup__

        sudo su

        apt-get update && apt-get upgrade -y

        # Edit /etc/dhcpcd.conf to set static IP

        reboot

  __Update and Upgrade__

        apt-get update && sudo apt-get upgrade

  __Download and Install Docker on Raspberry Pi__

        curl -fsSL https://get.docker.com -o get-docker.sh

        sudo sh get-docker.sh

  __Add a Non-Root User to the Docker Group__

        sudo usermod -aG docker [user_name]

        # To add the Pi user (the default user in Raspbian), use the command:

            sudo usermod -aG docker Pi

  __Check Docker Version and Info__

        docker version

        docker info

  __Run Hello World Container__

        docker run hello-world

  __How to Upgrade Docker on Raspberry Pi__

        apt-get upgrade

  __How to Uninstall Docker on Your Raspberry Pi__

        apt-get purge docker-ce

        rm -rf /var/lib/docker