---
title: ECryptfs
layout: default
---

<http://ubuntuforums.org/showthread.php?t=148600>

Install encfs

    apt-get install encfs

    mkdir -p ~/encrypted ~/temp_encr

Created encrypted dir / create password

    mount -t encfs ~/encrypted ~/temp_encr

Copy files to ~/temp\_encr

Umount encrypted dir

    fusermount -u ~/temp_encr
