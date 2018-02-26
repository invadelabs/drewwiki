---
title: GoogleCloud
layout: default
---

Download gcloud sdk
-------------------

-   <https://cloud.google.com/sdk/downloads#versioned>

Running gcloud
--------------

``` bash
# if needed $ export PATH=$PATH:~/google-cloud-sdk/bin

$ gcloud auth list
$ gcloud auth login
$ gcloud config set project drew-1298
$ gcloud compute instances list
$ gcloud compute ssh
$ gcloud compute ssh user@instance-1 --zone us-central1-a
```

Setup sendgrid email relay
--------------------------

<https://cloud.google.com/compute/docs/tutorials/sending-mail/using-sendgrid>

Install heirloom-mailx
----------------------

Needed to attach files via mailx, i.e.

``` bash
$ sudo apt-get install heirloom-mailx
$ echo "sqlite db drew.invadelabs.com" | mailx -a drew_wiki.sqlite.xz -s "sqlite db drew.invadelabs.com" drew@invadelabs.com
```
