---
title: MiniShift
layout: default
---

Install oc openshift client
===========================

Pull from [CLI tool](https://github.com/openshift/origin/releases)

Or from Red Hat
[1](https://docs.openshift.com/enterprise/3.0/cli_reference/get_started_cli.html)

Install Minishift
=================

Pull from
[github.com/minishift](https://github.com/minishift/minishift/releases)

Use Minishift with Virtual box
==============================

``` bash
minishift start --vm-driver=virtualbox
```

Login, deploy an app, expose, describe it
=========================================

``` bash
./oc login

./oc new-app centos/httpd-24-centos7~https://github.com/drew-holt/httpd-ex

./oc status

./oc expose svc/httpd-ex

./oc describe deploymentconfig httpd-ex
```
