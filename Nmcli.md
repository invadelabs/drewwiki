---
title: Nmcli
layout: default
---

``` bash
nmcli general status

nmcli connection show active

nmcli connection show configured

nmcli radio wifi

nmcli device wifi list

# nmcli device wifi connect drewfi password my_awesome_password
Connection with UUID '1234568-1234-1234-1234-123456789012' created and activated on device 'wlp0s4f1u2'

nmcli connection edit con-name <name of new connection>

nmcli connection edit con-name 1234568-1234-1234-1234-123456789012
```
