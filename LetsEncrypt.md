---
title: LetsEncrypt
layout: default
---

Instructions for Debian 9

certbot
-------

-   <https://certbot.eff.org/#debiantesting-apache>
-   <https://certbot.eff.org/docs/using.html>

### Install certbot

``` bash
sudo apt-get install python-certbot-apache certbot
```

### Obtain SNI Cert

Manually run due to existing configuration already redirecting port http
-&gt; https. Will require a small of downtime \`systemctl stop
apache2\`.

``` bash
certbot certonly --manual \
--cert-name invadelabs.com \
-d invadelabs.com \
-d www.invadelabs.com \
-d drew.invadelabs.com \
-d wiki.invadelabs.com \
-d blog.invadelabs.com \
-m drew@invadelabs.com \
--agree-tos
```

### Check newly Issue Cert

``` bash
root@invadelabs:~# certbot certificates
Saving debug log to /var/log/letsencrypt/letsencrypt.log

-------------------------------------------------------------------------------
Found the following certs:
  Certificate Name: invadelabs.com
    Domains: invadelabs.com drew.invadelabs.com
    Expiry Date: 2018-05-19 08:58:27+00:00 (VALID: 89 days)
    Certificate Path: /etc/letsencrypt/live/invadelabs.com/fullchain.pem
    Private Key Path: /etc/letsencrypt/live/invadelabs.com/privkey.pem
-------------------------------------------------------------------------------
```

### Test Renewal

Dry-run:

``` bash
$ sudo certbot renew --dry-run
```

### Renew Cert Manually

Will need to manually reload apache.

``` bash
$ sudo certbot renew
```

### Aapache Auto Renew On Cron

Add to root's cron and check twice daily:

``` bash
0 3,15 * * * certbot renew --apache --quiet 
```

### Expand Additional Domains SNI Cert

``` bash
certbot --expand -d invadelabs.com -d drew.invadelabs.com -d new.invadelabs.com
```

Old method
----------

``` bash
./letsencrypt-auto run --apache -d drew-bg.invadelabs.com

 - Congratulations! Your certificate and chain have been saved at
   /etc/letsencrypt/live/drew-bg.invadelabs.com/fullchain.pem. Your
   cert will expire on 2016-07-09. To obtain a new version of the
   certificate in the future, simply run Let's Encrypt again.

SSLCertificateFile /etc/letsencrypt/live/invadelabs.com/fullchain.pem
SSLCertificateKeyFile /etc/letsencrypt/live/invadelabs.com/privkey.pem
Include /etc/letsencrypt/options-ssl-apache.conf
```
