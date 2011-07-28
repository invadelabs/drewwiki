---
title: ApachePAMunixAuth
layout: default
---

    # yum install mod_auth_pam.x86_64 mod_auth_shadow.x86

<http://pam.sourceforge.net/mod_auth_pam/shadow.html>

Add to <Directory> or <Location>

        AuthPAM_Enabled on
        AuthShadow on
        AuthType "basic"
        AuthName "Auth"
        require user drew
        #require group blabla

    chmod 444 /etc/passwd

(orig 000) ---&gt; Find safe work around
