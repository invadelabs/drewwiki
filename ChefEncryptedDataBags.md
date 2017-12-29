---
title: ChefEncryptedDataBags
layout: default
---

Raw notes, needs formatting, context...

    ​
    $ openssl rand -base64 512 | tr -d '\r\n' > ~/encrypted_data_bag_secret
    $ knife data bag create --editor /usr/bin/vi --secret-file ./encrypted_data_bag_secret jenkins passwords
    $ knife data bag edit --editor /usr/bin/vi --secret-file ./encrypted_data_bag_secret jenkins passwords # do not mix up -s and --secret-file
    copy encrypted_data_bag_secret to chef-client:/etc/chef/encrypted_data_bag_secret

    {  
       "jenkins_invadelabs":{  
          "install_plugins":{  
             "plugins_list":[  
                "git"
             ]
          }
       }
    }

    knife data bag create --editor /usr/bin/vi --secret-file ./encrypted_data_bag_secret jenkins passwords
    knife data bag edit --editor /usr/bin/vi --secret-file ./encrypted_data_bag_secret jenkins passwords

    [2016-08-21T21:41:00-07:00] INFO: template[/apps/jenkins/hudson.plugins.sonar.SonarGlobalConfiguration.xml] sending restart action to service[jenkins] (delayed)
    Recipe: jenkins::_master_package
    * service[jenkins] action restart[2016-08-21T21:41:00-07:00] INFO: Processing service[jenkins] action restart (jenkins::_master_package line 74)
    [2016-08-21T21:41:00-07:00] DEBUG: Providers for generic service resource enabled on node include: [Chef::Provider::Service::Redhat, Chef::Provider::Service::Init]
    [2016-08-21T21:41:00-07:00] DEBUG: Provider for action restart on resource service[jenkins] is Chef::Provider::Service::Redhat
    [2016-08-21T21:41:00-07:00] DEBUG: service[jenkins] supports status, running
    jenkins (pid 21599) is running...