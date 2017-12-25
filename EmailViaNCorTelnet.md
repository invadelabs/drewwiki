---
title: EmailViaNCorTelnet
layout: default
---

Can always type quit instead of DATA if just checking possible to email

``` bash
$ nc localhost 25
220 invadelabscom ESMTP Postfix (Debian/GNU)
HELO somedomain.com
250 somedomain.com
mail from:<drew@somedomain.com>
250 2.1.0 Ok
rcpt to:<drewsemailaddress@gmail.com>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
From: [Drew Invade] <drew@somedomain.com>
To: [Drew Email Address] <drewsemailaddress@gmail.com>
Date: Fri, 22 Dec 2017 21:14:26 -0700
Subject: Sending from the command line!

Hi!
this is a test message using net cat lol. hope it works

.
250 2.0.0 Ok: queued as 03D8C82052

quit
221 2.0.0 Bye
```
