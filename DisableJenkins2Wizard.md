---
title: DisableJenkins2Wizard
layout: default
---

RHEL - Add to /etc/sysconfig/jenkins

JAVA\_ARGS=

``` bash
-Djenkins.install.runSetupWizard=false -Dhudson.InitReactorRunner.concurrency=24
```
