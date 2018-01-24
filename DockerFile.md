---
title: DockerFile
layout: default
---

**WIP** A very boring container that installs curl and npm.

Dockerfile
==========

    FROM ubuntu:16.04
    MAINTAINER Drew Holt <drew@invadelabs.com>

    RUN apt-get update && apt-get install curl npm -y

    ENV FOO bar

Build contanier
===============

    docker build -t drewderivative/mycontainer:0.0.1

Run container
=============

    docker run -p 8000:8888 drewderivative/mycontainer:0.0.1
