---
title: ChefMisc
layout: default
---

berkshelf selfhosted certificate authenticity
=============================================

    $ cat ~/.berkshelf/config.json
    {  
       "ssl":{  
          "verify":false
       }
    }

Freeze Chef cookbooks for versioning
====================================

​use -- freeze on knife cookbook upload job

Blurb
=====

    ​
    510 knife ssh "role:base" --ssh-user drew -P mypassword -y sudo service chef-client restart
    511 knife ssh "role:base" --ssh-user drew -P mypassword -y sudo chef-client
    knife-spork
    https://discourse.chef.io/t/ci-job-for-cookbook-version-increment-upload/4400/6
    http://lists.opscode.com/sympa/arc/chef/2013-08/msg00103.html
    ruby auto increment
    i += 1
    working ruby example http://www.hurryupandwait.io/blog/using-git-to-version-stamp-chef-artifacts
    https://github.com/GitTools/GitVersion
    sample ruby+thor example https://gist.github.com/mattray/7683491
    knife bootstrap jenkins-slave01.dev.invadelabs.com \
    -N jenkins-slave01-dev \
    -E dev \
    -r 'role[base], role[jenkins-slaves]' \
    --node-ssl-verify-mode none \
    --secret-file encrypted_data_bag_secret_sandbox \
    --ssh-user drew \
    --sudo \
    -y
    knife --bootstrap-version "x.y.z"
    knife bootstrap jenkins-slave01.prod.invadelabs.com \
    -N jenkins-slave01-production \
    -E production \
    -r 'role[base], role[jenkins-slaves], role[jenkins-add-new-slave]' \
    --node-ssl-verify-mode none \
    --secret-file encrypted_data_bag_secret_production \
    --ssh-user drew \
    --sudo \
    -y
    rubocop -D
    --display-cop-names
    don't forget to:
    service chef-client start
    /etc/chef/client.conf thing or somethi
    chef.log_level = :debug
    chef.add_recipe 'mysql-invadelabs'

    sudo chef gem install --no-user-install knife-spork
    sudo chef gem install --no-user-install slack-notifier
    knife spork check jenkins-invadelabs
    if [ `git log --pretty=oneline | head -1 | grep "#major"` ]
    then
    knife spork bump jenkins-invadelabs major
    elif [ `git log --pretty=oneline | head -1 | grep "#minor"` ]
    then
    knife spork bump jenkins-invadelabs minor
    elif [ `git log --pretty=oneline | head -1 | grep "#patch"` ]
    then
    knife spork bump jenkins-invadelabs patch
    else
    knife spork bump jenkins-invadelabs patch
    knife spork upload jenkins-invadelabs
    #knife spork promote sandbox jenkins-invadelabs --remote
    chef exec gem install hip chat

    sudo yum-config-manager --enable docker
    chef exec rake -T 
