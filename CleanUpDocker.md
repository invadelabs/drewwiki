---
title: CleanUpDocker
layout: default
---

Remove all containers then remove all images

    $ docker ps -a | cut -f 1 -d" " | xargs docker rm
    $ docker images | awk '{print $3}' | xargs docker rmi

Work around:

     
    docker ps -a -f status=dead -q | xargs -r -I % bash -c 'rm -rf /srv/docker/overlay/%1*'
    docker ps -a -f status=dead -q | xargs -r docker rm -f -v
