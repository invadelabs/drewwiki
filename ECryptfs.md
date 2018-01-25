---
title: ECryptfs
layout: default
---

ecryptfs
--------

``` bash
sudo apt-get install ecryptfs-utils
ecryptfs-setup-private
umount.ecryptfs_private
mount.ecryptfs_private
```

encfs
-----

<http://ubuntuforums.org/showthread.php?t=148600>

Install encfs

``` bash
apt-get install encfs
mkdir -p ~/encrypted ~/temp_encr
```

Created encrypted dir / create password

``` bash
encfs ~/encrypted ~/temp_encr
```

Copy files to ~/temp\_encr

Umount encrypted dir

``` bash
fusermount -u ~/temp_encr
```
