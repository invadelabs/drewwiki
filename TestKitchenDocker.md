---
title: TestKitchenDocker
layout: default
---

Use ChefDk to install kitchen-docker into Chef's ruby omnibus

``` bash
sudo chef gem install kitchen-docker
```

``` bash
sudo chef kitchen test
```

.kitchen.yml in repo

``` bash
---
driver:
  name: docker
  use_sudo: false

platforms:
  - name: centos-7.2

driver_config:
  require_chef_omnibus: 12.16.42
  provision_command: 'yum install initscripts -y'
  run_command: '/usr/sbin/init'
  privileged: true

suites:
  - name: jenkins-invadelabs
    data_bags_path: 'test/integration/data_bags'
    encrypted_data_bag_secret_key_path: "test/integration/encrypted_data_bag_secret"
    attributes:
      java:
        jdk_version: "8"
```
