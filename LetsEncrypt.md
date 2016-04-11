---
title: LetsEncrypt
layout: default
---

<https://letsencrypt.org/howitworks/>

    $ git clone https://github.com/letsencrypt/letsencrypt
    $ cd letsencrypt
    $ ./letsencrypt-auto --help
    $ ./letsencrypt-auto --apache
    IMPORTANT NOTES:
     - Congratulations! Your certificate and chain have been saved at
       /etc/letsencrypt/live/drew.invadelabs.com/fullchain.pem. Your cert
       will expire on 2016-05-15. To obtain a new version of the
       certificate in the future, simply run Let's Encrypt again.
     - If you like Let's Encrypt, please consider supporting our work by:

       Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
       Donating to EFF:                    https://eff.org/donate-le

Per domain:

    ./letsencrypt-auto run --apache -d drew-bg.invadelabs.com

     - Congratulations! Your certificate and chain have been saved at
       /etc/letsencrypt/live/drew-bg.invadelabs.com/fullchain.pem. Your
       cert will expire on 2016-07-09. To obtain a new version of the
       certificate in the future, simply run Let's Encrypt again.

    SSLCertificateFile /etc/letsencrypt/live/drew-bg.invadelabs.com/fullchain.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/drew-bg.invadelabs.com/privkey.pem
    Include /etc/letsencrypt/options-ssl-apache.conf
