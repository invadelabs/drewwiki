---
title: LetsEncrypt
layout: default
---

certbot
-------

-   <https://certbot.eff.org/#debianjessie-apache>

### Install certbot

    $ sudo apt-get install certbot

### Obtain / Renew certs

Dry-run:

    $ sudo certbot renew --dry-run

Update:

    $ sudo certbot renew

Add to root's cron and check twice daily:

    0 3,15 * * * certbot renew --quiet 

Old method
----------

    ./letsencrypt-auto run --apache -d drew-bg.invadelabs.com

     - Congratulations! Your certificate and chain have been saved at
       /etc/letsencrypt/live/drew-bg.invadelabs.com/fullchain.pem. Your
       cert will expire on 2016-07-09. To obtain a new version of the
       certificate in the future, simply run Let's Encrypt again.

    SSLCertificateFile /etc/letsencrypt/live/drew-bg.invadelabs.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/drew-bg.invadelabs.com/privkey.pem
    Include /etc/letsencrypt/options-ssl-apache.conf
