---
title: Lxc
layout: default
---

Create container
----------------

``` bash
drew@drew-itx:~$ sudo lxc-create -n test-container -t ubuntu
Checking cache download in /var/cache/lxc/trusty/rootfs-amd64 ...
Installing packages in template: ssh,vim,language-pack-en
Downloading ubuntu trusty minimal ...
I: Retrieving Release
I: Retrieving Release.gpg
I: Checking Release signature
I: Valid Release signature (key id 790BC7277767219C42C86F933B4FE6ACC0B21F32)
I: Retrieving Packages
I: Validating Packages
I: Retrieving Packages
I: Validating Packages
I: Resolving dependencies of required packages...
I: Resolving dependencies of base packages...
```

Show containers status
----------------------

``` bash
# lxc-ls --fancy
```

Start Container w/ Console
--------------------------

``` bash
# lxc-start -n test-container -d
```

Connect to console
------------------

``` bash
# lxc-console -n test-container
```

Exit by typing Ctrl-A followed by Q

shutdown (lxc-stop for instant shutdown)
----------------------------------------

``` bash
# lxc-shutdown -n test-container
```

delete
------

``` bash
lxc-destroy -n test-container
```

Configuration
-------------

config is /var/lib/lxc/test-container/config

to auto start

``` bash
ln -s /var/lib/lxc/test-container/config /etc/lxc/auto/test-container.conf
```

Port forward to container
-------------------------

``` bash
$ iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to 10.0.3.143:80
$ iptables -t nat -A PREROUTING -p tcp -i eth0 --dport 10022 -j DNAT --to-destination 10.0.3.239:22
```
