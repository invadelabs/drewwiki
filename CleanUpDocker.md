---
title: CleanUpDocker
layout: default
---

Remove all containers then remove all images

    $ docker ps -a | cut -f 1 -d" " | xargs docker rm
    $ docker images | awk '{print $3}' | xargs docker rmi
