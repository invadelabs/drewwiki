---
title: TerraformExamples
layout: default
---

Terraform Examples
==================

Setup
-----

### Download Terraform

    $ mkdir ~/terraform && cd ~/terraform
    $ curl -o terraform http://....
    $ chmod 755 terraform

### terraform init

    drew@drew-8570w:~/terraform$ ./terraform init

    Initializing provider plugins...
    - Checking for available provider plugins on https://releases.hashicorp.com...
    - Downloading plugin for provider "aws" (1.7.1)...

    The following providers do not have any version constraints in configuration,
    so the latest version was installed.

    To prevent automatic upgrades to new major versions that may contain breaking
    changes, it is recommended to add version = "..." constraints to the
    corresponding provider blocks in configuration, with the constraint strings
    suggested below.

    * provider.aws: version = "~> 1.7"

    Terraform has been successfully initialized!

    You may now begin working with Terraform. Try running "terraform plan" to see
    any changes that are required for your infrastructure. All Terraform commands
    should now work.

    If you ever set or change modules or backend configuration for Terraform,
    rerun this command to reinitialize your working directory. If you forget, other
    commands will detect it and remind you to do so if necessary.

### terraform plan

    drew@drew-8570w:~/terraform$ ./terraform plan
    Refreshing Terraform state in-memory prior to plan...
    The refreshed state will be used to calculate this plan, but will not be
    persisted to local or remote state storage.


    ------------------------------------------------------------------------

    An execution plan has been generated and is shown below.
    Resource actions are indicated with the following symbols:
      + create

    Terraform will perform the following actions:

      + aws_instance.invadelabs-web001
          id:                                        <computed>
          ami:                                       "ami-93ed5feb"
          associate_public_ip_address:               <computed>
          availability_zone:                         <computed>
          ebs_block_device.#:                        <computed>
          ephemeral_block_device.#:                  <computed>
          instance_state:                            <computed>
          instance_type:                             "t2.micro"
          ipv6_address_count:                        <computed>
          ipv6_addresses.#:                          <computed>
          key_name:                                  "drew-2018.01.09-us-west-2"
          network_interface.#:                       <computed>
          network_interface_id:                      <computed>
          placement_group:                           <computed>
          primary_network_interface_id:              <computed>
          private_dns:                               <computed>
          private_ip:                                <computed>
          public_dns:                                <computed>
          public_ip:                                 <computed>
          root_block_device.#:                       "1"
          root_block_device.0.delete_on_termination: "true"
          root_block_device.0.volume_id:             <computed>
          root_block_device.0.volume_size:           "8"
          root_block_device.0.volume_type:           <computed>
          security_groups.#:                         <computed>
          source_dest_check:                         "true"
          subnet_id:                                 <computed>
          tags.%:                                    "1"
          tags.Name:                                 "invadelabs-web001"
          tenancy:                                   <computed>
          volume_tags.%:                             <computed>
          vpc_security_group_ids.#:                  <computed>


    Plan: 1 to add, 0 to change, 0 to destroy.

    ------------------------------------------------------------------------

    Note: You didn't specify an "-out" parameter to save this plan, so Terraform
    can't guarantee that exactly these actions will be performed if
    "terraform apply" is subsequently run.

### terraform apply

    drew@drew-8570w:~/terraform$ ./terraform apply

    An execution plan has been generated and is shown below.
    Resource actions are indicated with the following symbols:
      + create

    Terraform will perform the following actions:

      + aws_instance.invadelabs-web001
          id:                                        <computed>
          ami:                                       "ami-93ed5feb"
          associate_public_ip_address:               <computed>
          availability_zone:                         <computed>
          ebs_block_device.#:                        <computed>
          ephemeral_block_device.#:                  <computed>
          instance_state:                            <computed>
          instance_type:                             "t2.micro"
          ipv6_address_count:                        <computed>
          ipv6_addresses.#:                          <computed>
          key_name:                                  "drew-2018.01.09-us-west-2"
          network_interface.#:                       <computed>
          network_interface_id:                      <computed>
          placement_group:                           <computed>
          primary_network_interface_id:              <computed>
          private_dns:                               <computed>
          private_ip:                                <computed>
          public_dns:                                <computed>
          public_ip:                                 <computed>
          root_block_device.#:                       "1"
          root_block_device.0.delete_on_termination: "true"
          root_block_device.0.volume_id:             <computed>
          root_block_device.0.volume_size:           "8"
          root_block_device.0.volume_type:           <computed>
          security_groups.#:                         <computed>
          source_dest_check:                         "true"
          subnet_id:                                 <computed>
          tags.%:                                    "1"
          tags.Name:                                 "invadelabs-web001"
          tenancy:                                   <computed>
          volume_tags.%:                             <computed>
          vpc_security_group_ids.#:                  <computed>


    Plan: 1 to add, 0 to change, 0 to destroy.

    Do you want to perform these actions?
      Terraform will perform the actions described above.
      Only 'yes' will be accepted to approve.

      Enter a value: yes

    aws_instance.invadelabs-web001: Creating...
      ami:                                       "" => "ami-93ed5feb"
      associate_public_ip_address:               "" => "<computed>"
      availability_zone:                         "" => "<computed>"
      ebs_block_device.#:                        "" => "<computed>"
      ephemeral_block_device.#:                  "" => "<computed>"
      instance_state:                            "" => "<computed>"
      instance_type:                             "" => "t2.micro"
      ipv6_address_count:                        "" => "<computed>"
      ipv6_addresses.#:                          "" => "<computed>"
      key_name:                                  "" => "drew-2018.01.09-us-west-2"
      network_interface.#:                       "" => "<computed>"
      network_interface_id:                      "" => "<computed>"
      placement_group:                           "" => "<computed>"
      primary_network_interface_id:              "" => "<computed>"
      private_dns:                               "" => "<computed>"
      private_ip:                                "" => "<computed>"
      public_dns:                                "" => "<computed>"
      public_ip:                                 "" => "<computed>"
      root_block_device.#:                       "" => "1"
      root_block_device.0.delete_on_termination: "" => "true"
      root_block_device.0.volume_id:             "" => "<computed>"
      root_block_device.0.volume_size:           "" => "8"
      root_block_device.0.volume_type:           "" => "<computed>"
      security_groups.#:                         "" => "<computed>"
      source_dest_check:                         "" => "true"
      subnet_id:                                 "" => "<computed>"
      tags.%:                                    "" => "1"
      tags.Name:                                 "" => "invadelabs-web001"
      tenancy:                                   "" => "<computed>"
      volume_tags.%:                             "" => "<computed>"
      vpc_security_group_ids.#:                  "" => "<computed>"
    aws_instance.invadelabs-web001: Still creating... (10s elapsed)
    aws_instance.invadelabs-web001: Still creating... (20s elapsed)
    aws_instance.invadelabs-web001: Creation complete after 25s (ID: i-08e94c2ef875fe3fa)

    Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

### terraform show

    drew@drew-8570w:~/terraform$ ./terraform show
    aws_instance.invadelabs-web001:
      id = i-0168a6fa363df0156
      ami = ami-93ed5feb
      associate_public_ip_address = true
      availability_zone = us-west-2b
      disable_api_termination = false
      ebs_block_device.# = 0
      ebs_optimized = false
      ephemeral_block_device.# = 0
      iam_instance_profile = 
      instance_state = running
      instance_type = t2.micro
      ipv6_addresses.# = 0
      key_name = drew-2018.01.09-us-west-2
      monitoring = false
      network_interface.# = 0
      network_interface_id = eni-d47d49e1
      placement_group = 
      primary_network_interface_id = eni-d47d49e1
      private_dns = ip-172-31-16-154.us-west-2.compute.internal
      private_ip = 172.31.16.154
      public_dns = ec2-54-202-253-83.us-west-2.compute.amazonaws.com
      public_ip = 54.202.253.83
      root_block_device.# = 1
      root_block_device.0.delete_on_termination = true
      root_block_device.0.iops = 0
      root_block_device.0.volume_id = vol-0d601b4beac484763
      root_block_device.0.volume_size = 8
      root_block_device.0.volume_type = standard
      security_groups.# = 1
      security_groups.3814588639 = default
      source_dest_check = true
      subnet_id = subnet-a9ea23de
      tags.% = 1
      tags.name = invadelabs-web001
      tenancy = default
      volume_tags.% = 0
      vpc_security_group_ids.# = 0

### terraform destroy

drew@drew-8570w:~/terraform$ ./terraform destroy
aws\_instance.invadelabs-web001: Refreshing state... (ID:
i-08e94c2ef875fe3fa)

An execution plan has been generated and is shown below. Resource
actions are indicated with the following symbols:

` - destroy`

Terraform will perform the following actions:

` - aws_instance.invadelabs-web001`

Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy?

` Terraform will destroy all your managed infrastructure, as shown above.`  
` There is no undo. Only 'yes' will be accepted to confirm.`

` Enter a value: yes`

aws\_instance.invadelabs-web001: Destroying... (ID: i-08e94c2ef875fe3fa)
aws\_instance.invadelabs-web001: Still destroying... (ID:
i-08e94c2ef875fe3fa, 10s elapsed) aws\_instance.invadelabs-web001: Still
destroying... (ID: i-08e94c2ef875fe3fa, 20s elapsed)
aws\_instance.invadelabs-web001: Still destroying... (ID:
i-08e94c2ef875fe3fa, 30s elapsed) aws\_instance.invadelabs-web001: Still
destroying... (ID: i-08e94c2ef875fe3fa, 40s elapsed)
aws\_instance.invadelabs-web001: Still destroying... (ID:
i-08e94c2ef875fe3fa, 50s elapsed) aws\_instance.invadelabs-web001: Still
destroying... (ID: i-08e94c2ef875fe3fa, 1m0s elapsed)
aws\_instance.invadelabs-web001: Destruction complete after 1m3s

Destroy complete! Resources: 1 destroyed.

</syntaxhighlight>
Configuration
-------------

example.tf file
---------------

    drew@drew-8570w:~/terraform$ cat example.tf 
    provider "aws" {
      access_key = "MYAWSACCESSKEY"
      secret_key = "MYAWSSECRETKEY"
      region     = "us-west-2"
    }

    # variable "ami" {
    #   ami = "ami-93ed5feb"
    #   description = "Amazon Linux w/ httpd and php"
    # }

    resource "aws_instance" "invadelabs-web001" {
      # ami = "${var.ami}"
      ami = "ami-93ed5feb"
      instance_type = "t2.micro"
      count = 1
      key_name = "drew-2018.01.01-us-west-2"

      root_block_device = {
        volume_size = 8
      }

      # security_groups.# = 1

      tags {
        Name = "invadelabs-web001"
      }

      # subnet = "${var.env == "production" ? var.prod_subnet : var.dev_subnet}"
      # source_dest_check = false

      connection {
        user = "ec2-user"
      }
    }

    # resource "aws_key_pair" "deployer" {
    #   key_name   = "deployer-key"
    #   public_key = "ssh-rsa AAAAB3NzaC1yc...  email@example.com"
    # }
