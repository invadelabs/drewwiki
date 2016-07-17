---
title: DockerOnUbuntu
layout: default
---

Installation
============

    # curl -fsSL https://get.docker.com/ | sh
    ...
    + sudo -E sh -c docker version
    Client:
     Version:      1.10.1
     API version:  1.22
     Go version:   go1.5.3
     Git commit:   9e83765
     Built:        Thu Feb 11 19:32:54 2016
     OS/Arch:      linux/amd64

    Server:
     Version:      1.10.1
     API version:  1.22
     Go version:   go1.5.3
     Git commit:   9e83765
     Built:        Thu Feb 11 19:32:54 2016
     OS/Arch:      linux/amd64

    If you would like to use Docker as a non-root user, you should now consider
    adding your user to the "docker" group with something like:

      sudo usermod -aG docker drew

    Remember that you will have to log out and back in for this to take effect!

Download a container
====================

Download a container and run bash (-i interactive, -t tty)

    $ docker run -it ubuntu bash

Enable Rest API
===============

<http://www.campalus.com/enable-remote-tcp-connections-to-docker-host-running-ubuntu-15-04/>

Advanced Rest Client Application (Chrome)
=========================================

    http://drew-desktop:4243/images/json