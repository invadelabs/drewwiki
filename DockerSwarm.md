---
title: DockerSwarm
layout: default
---

Simple Swarm Example

``` bash
docker swarm init
docker network create --driver overlay mynet
docker service create --replicas 3 --name redis --network mynet --update-delay 10s -p 6379:6379 redis:3.0.6
docker network create --driver overlay --attachable redis
```
