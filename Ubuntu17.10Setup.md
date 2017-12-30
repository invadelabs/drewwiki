---
title: Ubuntu17.10Setup
layout: default
---

After initial install
=====================

    sudo apt-get update
    sudo apt-get upgrade -y
    sudo apt-get dist-upgrade

    sudo apt-get install -y etckeeper
    cd /etc
    sudo etckeeper init
    sudo vi .gitignore # remove sensitive files

Disable Guest Login
-------------------

    sudo sh -c "echo 'allow-guest=false' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"

Show username in Desktop Manager
--------------------------------

    gsettings set com.canonical.indicator.session show-real-name-on-panel true

Set vim Editor
--------------

    sudo update-alternatives --set editor /usr/bin/vim.basic

Set passwordless sudo
---------------------

    visudo:
    username ALL=(ALL) NOPASSWD: ALL

Install Main Apps
=================

    sudo apt-get install \
    keepass2 rdesktop vncviewer \
    lm-sensors p7zip-full exfat-utils exfat-fuse \
    vim ssh git \
    ubuntu-restricted-extras qbittorrent gimp audacity \ 
    icedtea-8-plugin \
    network-manager-openvpn wireshark  nmap \
    openvpn openssh-server fail2ban \
    vlc vlc-plugin-fluidsynth ffmpeg atomicparsley \
    chrome-gnome-shell \
    gnome-tweaks

    ** VirtualBox
    ** Chrome, verify Google Hangouts
    ** Insynq
    ** Atom
    ** Synergy
    ** Ramlog or equivalent for SSD
    ** nvm
    ** rvm
    ** sqlitebrowser
    ** Studio 3T (mongodb browswer)
    ** IntelliJ
    ** Android Studio

    oracle-java8-installer
    cairo-dock
    adobe-flashplugin
    encfs youtube-dl nikto exiftool chkrootkit apache2-utils pidgin wavemon xd docker.io virtualenv python2.7-examples mailutils ansible namebench python-pip (via apt)
    xchat
    youtube-dl

Other
=====

    sudo apt-get install -y nfs-common cifs-utils ethtool pm-utils

Other Configuration
===================

Remote syslog

    echo "*.* @192.168.1.200" >> /etc/rsyslog.d/50-default.conf

-   tmpfs for /tmp and (maybe make this a bind mount..)

<!-- -->

    tmpfs   /tmp       tmpfs   defaults,noatime,mode=1777   0  0

-   /etc/fstab

<!-- -->

    192.168.1.200:/mnt/raid5 /mnt/raid5 nfs defaults    0 0

-   web server if needed

<!-- -->

    sudo apt-get install apache2 php5 php5-sqlite
