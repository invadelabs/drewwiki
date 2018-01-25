---
title: CentOS7Docker
layout: default
---

Add Docker YUM Repo
===================

``` bash
sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enabled=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg
EOF
```

Install Docker
==============

``` bash
sudo yum install -y docker-engine
sudo mkdir /srv/docker
sudo mkdir /etc/systemd/system/docker.service.d
```

Move standard mount point
-------------------------

``` bash
sudo vi /etc/systemd/system/docker.service.d/graph.conf
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --graph="/srv/docker" --storage-driver=overlay
```

Reload, enable, and start the daemon
------------------------------------

``` bash
sudo systemctl daemon-reload
sudo systemctl enable docker.service
sudo systemctl start docker
```

Install EPEL for PIP
====================

``` bash
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum --disablerepo="*" --enablerepo="epel" install -y python-pip
```

Install docker-compose via pip
------------------------------

``` bash
yum upgrade python-*
sudo yum install -y git # not installed on minimal
sudo pip install docker-compose
```

Add docker group
================

``` bash
sudo groupadd docker
```

Add user to group
-----------------

``` bash
useradd -m drew
sudo usermod -aG docker drew
```

Misc
====

``` bash
docker ps | grep mongo # find container id
docker exec -t -i 7f71cedafaab bash
mongo 172.17.0.2/admin --eval 'db.getSiblingDB("dashboard").createUser({user: "db", pwd: "dbpass", roles: [{role: "readWrite", db: "dashboard"}]})'
^ change to localhost
```
