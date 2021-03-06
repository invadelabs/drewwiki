---
title: ChefJenkinsGroovyShellOut
layout: default
---

``` bash
​
java -jar /opt/jenkins-cli.jar -s http://localhost:8080 help --username admin
java -jar /opt/jenkins-cli.jar -s http://localhost:8080 groovy bla.txt --username admin
java -jar /opt/jenkins-cli.jar -s http://localhost:8080 groovy crypt.groovy --username admin --password-file jenkins_pass.txt
=========================
```

``` groovy
import com.trilead.ssh2.crypto.Base64;
import javax.crypto.Cipher;
import jenkins.security.CryptoConfidentialKey;
import hudson.util.Secret;
CryptoConfidentialKey KEY = new CryptoConfidentialKey(Secret.class.getName());
Cipher cipher = KEY.encrypt();
String MAGIC = "::::MAGIC::::";
String VALUE_TO_ENCRYPT = "my secret key goes here";
println(new String(Base64.encode(cipher.doFinal((VALUE_TO_ENCRYPT + MAGIC).getBytes("UTF-8")))));
=========================
```

``` ruby
ruby_block "something" do
block do
#tricky way to load this Chef::Mixin::ShellOut utilities
Chef::Resource::RubyBlock.send(:include, Chef::Mixin::ShellOut)
command = 'cat /etc/hostname'
command_out = shell_out(command)
node.set['my_attribute'] = command_out.stdout
end
action :create
end
=========================
```

``` groovy
UNENC_PW="admin"
cat <<EOF | java -jar /opt/jenkins-cli.jar -s http://localhost:8080 groovy =
import com.trilead.ssh2.crypto.Base64;
import javax.crypto.Cipher;
import jenkins.security.CryptoConfidentialKey;
import hudson.util.Secret;
CryptoConfidentialKey KEY = new CryptoConfidentialKey(Secret.class.getName());
Cipher cipher = KEY.encrypt();
String MAGIC = "::::MAGIC::::";
String VALUE_TO_ENCRYPT = "$UNENC_PW";
println(new String(Base64.encode(cipher.doFinal((VALUE_TO_ENCRYPT + MAGIC).getBytes("UTF-8")))));
EOF
=========================
```
