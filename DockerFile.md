---
title: DockerFile
layout: default
---

**WIP** A very boring container that installs curl and npm.

Dockerfile
==========

``` bash
FROM ubuntu:16.04
MAINTAINER Drew Holt <drew@invadelabs.com>

RUN apt-get update && apt-get install curl npm -y

ENV foo /bar
WORKDIR ${foo}   # WORKDIR /bar
ADD . $foo       # ADD . /bar
COPY \$foo /myapp # COPY $foo /myapp

RUN /myapp/myapp
```

Build contanier
===============

``` bash
docker build -t drewderivative/mycontainer:0.0.1
```

Run container
=============

``` bash
docker run -p 8000:8888 drewderivative/mycontainer:0.0.1
```
