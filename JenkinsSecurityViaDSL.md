---
title: JenkinsSecurityViaDSL
layout: default
---

Jenkins Groovy DSL to change security to role strategy

**Notes:** Role strategy plugin must be installed

``` bash
import jenkins.model.*
import hudson.security.*
import com.michelin.cio.hudson.plugins.rolestrategy.*
def instance = Jenkins.getInstance()
def hudsonRealm = new HudsonPrivateSecurityRealm(false)
instance.setSecurityRealm(hudsonRealm)
def strategy = new RoleBasedAuthorizationStrategy()
strategy.add(Jenkins.ADMINISTER, "admin")
instance.setAuthorizationStrategy(strategy)
instance.save()
```
