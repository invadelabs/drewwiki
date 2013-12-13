---
title: Ddwrt-ddns-namecheap
layout: default
---

NameCheap.com Dynamic DNS
-------------------------

DD-WRT DDNS Configuration Page

    DDNS Service:  Custom
    DYNDNS Server:  dynamicdns.park-your-domain.com
    Username:   (Any jibberish can go here.)
    Password:   [Your NameCheap-defined Dynamic DNS password]
    Host Name:  [Your subdomain ('www' for the standard, or '@' for no subdomain)]
    URL:        /update?domain=[your domain]&password=[your password]&host=
    Password    12345678901234567890123456789012

Manually via curl
-----------------

    curl -s http://dynamicdns.park-your-domain.com/update?domain=readytoinvade.com&password=12345678901234567890123456789012&host=drewpi

External IP check for domain: readytoinvade.com host: drewpi

-   **Note** watch for trailing space on password!

