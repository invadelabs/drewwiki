---
title: InstallingChefServer
layout: default
---

Installation of Chef Server on CentOS6 with install target as /apps
directory.

Configure Postfix
=================

Add to /etc/postfix/main.cf:

``` bash
relayhost = mail.invadelabs.org
```

Enable, start, test

``` bash
sudo chkconfig postfix on
sudo service postfix start
echo "test message" | mailx -s test drew@invadelabs.com
```

Install Chef
============

Work around to install in another directory

``` bash
sudo ln -s /apps/opt/opscode/ /opt/opscode
cd /apps
wget https://packages.chef.io/stable/el/6/chef-server-core-12.8.0-1.el6.x86_64.rpm
sudo rpm -Uvh --prefix /apps chef-server-core-12.8.0-1.el6.x86_64.rpm
```

Configure Chef Server
=====================

Set configuration

``` bash
[root@chef private]# cat /etc/opscode/chef-server.rb
api_fqdn "chef.invadelabs.com"
nginx['ssl_certificate'] = "/etc/pki/tls/private/chef.invadelabs.com.pem"
nginx['ssl_certificate_key'] = "/etc/pki/tls/private/chef.invadelabs.com.nopassphrase.key"
nginx['ssl_ciphers'] = "HIGH:MEDIUM:!LOW:!kEDH:!aNULL:!ADH:!eNULL:!EXP:!SSLv2:!SEED:!CAMELLIA:!PSK"
nginx['ssl_protocols'] = "TLSv1 TLSv1.1 TLSv1.2"
```

Reconfigure Chef Server with our keys

``` bash
sudo chef-server-ctl reconfigure
```

Configure First User
====================

``` bash
chef-server-ctl user-create drewholt Drew Holt drew@invadelabs.com 'myawesomepassword' --filename drewholt.pem
```

Install Chef Manage
===================

``` bash
cd /apps
wget https://packages.chef.io/stable/el/6/chef-manage-2.4.1-1.el6.x86_64.rpm
sudo rpm -Uvh --prefix /apps chef-manage-2.4.1-1.el6.x86_64.rpm
sudo chef-server-ctl reconfigure
sudo chef-manage-ctl reconfigure
```

Install OpsCode Reporting
=========================

``` bash
cd /apps
wget https://packages.chef.io/stable/el/6/opscode-reporting-1.6.0-1.el6.x86_64.rpm
sudo rpm -Uvh --prefix /apps opscode-reporting-1.6.0-1.el6.x86_64.rpm
sudo ln -s /apps/opt/chef-manage /opt/chef-manage
sudo ln -s /apps/opt/opscode-reporting /opt/opscode-reporting
```

Create First Chef org
=====================

``` bash
chef-server-ctl org-create short_name 'full_organization_name' --association_user user_name --filename ORGANIZATION-validator.pem
```

Backup and Restore Chef Server
==============================

Backup

``` bash
sudo chef-server-ctl backup
```

Restore

``` bash
sudo chef-server-ctl restore -c -d /apps/tmp chef-backup-2016-10-14-17-30-38.tgz
```
