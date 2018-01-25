---
title: ApachePAMunixAuth
layout: default
---

``` bash
$ sudo yum install mod_auth_pam.x86_64 mod_auth_shadow.x86
```

<http://pam.sourceforge.net/mod_auth_pam/shadow.html>

Add to <Directory> or <Location>

``` bash
    AuthPAM_Enabled on
    AuthShadow on
    AuthType "basic"
    AuthName "Auth"
    require user drew
    #require group blabla
```

Find safe work around
=====================

``` bash
chmod 440 /etc/passwd
```

(orig 400)
