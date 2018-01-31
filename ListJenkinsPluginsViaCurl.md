---
title: ListJenkinsPluginsViaCurl
layout: default
---

​Get list of install plugins

``` bash
export JENKINS_HOST=admin:my_awesome_password@localhost:8080
```

``` bash
curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/'
JENKINS_HOST=localhost:8080
```

Example output

``` bash
ace-editor:1.1 aws-java-sdk:1.11.37 bouncycastle-api:2.16.0 branch-api:1.11 cloudbees-folder:5.13 conditional-buildstep:1.3.5 copyartifact:1.38.1 credentials:2.1.8 display-url-api:0.5 durable-task:1.12 git:3.0.0 git-client:2.0.0 git-server:1.7 github:1.22.3 github-api:1.79 handlebars:1.1.1 icon-shim:2.0.3 jackson2-api:2.7.3 javadoc:1.4 job-dsl:1.52 jquery:1.11.2-0 jquery-detached:1.2.1 junit:1.19 mailer:1.18 matrix-auth:1.4 matrix-project:1.7.1 maven-plugin:2.14 momentjs:1.1.1 naginator:1.17.2 parameterized-trigger:2.32 pipeline-build-step:2.3 pipeline-graph-analysis:1.1 pipeline-input-step:2.3 pipeline-milestone-step:1.1 pipeline-rest-api:2.2 pipeline-stage-step:2.2 pipeline-stage-view:2.0 plain-credentials:1.3 run-condition:1.0 s3:0.10.10 scm-api:1.3 script-security:1.24 sonar:2.5 ssh-credentials:1.12 structs:1.5 token-macro:2.0 workflow-aggregator:2.4 workflow-api:2.5 workflow-basic-steps:2.3 workflow-cps:2.17 workflow-cps-global-lib:2.3 workflow-durable-task-step:2.5 workflow-job:2.8 workflow-multibranch:2.8 workflow-scm-step:2.2 workflow-step-api:2.5 workflow-support:2.10
```

All on one line with = separator for version

``` bash
curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /=/' | sed ':a;N;$!ba;s/\n/ /g'
```
