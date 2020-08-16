---
title: Main Page
layout: default
---

A collection of randomness I've encountered and configured in Linux. -
drew@invadelabs.com

System Setup
------------

Now done via
[invadelabs/ansible-invadelabs](https://github.com/invadelabs/ansible-invadelabs)

-   [ServerSetupCentOS7](ServerSetupCentOS7.md "wikilink") - CentOS7 Server
    setup with NFS/rsyslog/chrony/hw\_mon services + qemu+kvm libvirt +
    Puppet + Foreman + Docker
-   [ServerSetupFedora27](ServerSetupFedora27.md "wikilink") - Fedora 27
    Server Setup

Infrastructure
--------------

### Infrastructure Automation

#### Chef

-   [InstallingChefServer](InstallingChefServer.md "wikilink") - Installing
    Chef Server
-   [KnifeBootstrapAWS](KnifeBootstrapAWS.md "wikilink") - knife
    bootstrapping AWS instances
-   [ChefEncryptedDataBags](ChefEncryptedDataBags.md "wikilink") - Creating
    and using encrypted data bags
-   [FoodcriticRubocop](FoodcriticRubocop.md "wikilink") - Linting recipes
    with Foodcritic and Rubocop
-   [TestingWithChefSpec](TestingWithChefSpec.md "wikilink") - Examples of
    using ChefSpec for unit and integration tests in cookbooks
-   [TestKitchenVagrant](TestKitchenVagrant.md "wikilink") - Test Kitchen
    with Vagrant provisioner for testing cookbooks
-   [TestKitchenDocker](TestKitchenDocker.md "wikilink") - Test Kitchen
    with Docker provisioner for testing cookbooks
-   [ChefJenkinsGroovyShellOut](ChefJenkinsGroovyShellOut.md "wikilink") -
    Shell out of recipe to use jenkins-cli to grab the encrypted or
    unencrytped value of a secret using Jenkins Groovy
-   [ChefMisc](ChefMisc.md "wikilink") - Misc Chef

#### Puppet

-   [MultiMachineVagrantPuppetJenkinsNexus](MultiMachineVagrantPuppetJenkinsNexus.md "wikilink") -
    Multimachine Vagrant boxes with 1 Puppet Server, 1 Puppet Client,
    and 1 Jenkins/Nexus VM to deploy Tomcat via Puppet

#### Ansible

-   [AnsibleVirtualboxDocker](https://github.com/drew-holt/ansible-invadelabs) -
    GitHub: Invade Labs test environment for Ansible with VirtualBox VMs
    running Docker in a dind cluster

#### Terraform

-   [TerraformExamples](TerraformExamples.md "wikilink") - Terraform
    examples placeholder

#### Jenkins

-   [DisableJenkins2Wizard](DisableJenkins2Wizard.md "wikilink") - Disable
    Jenkins 2.0 Setup Wizard
-   [JenkinsSecurityViaDSL](JenkinsSecurityViaDSL.md "wikilink") - Jenkins
    Security via DSL
-   [ListJenkinsPluginsViaCurl](ListJenkinsPluginsViaCurl.md "wikilink") -
    List Jenkins plugins via curl

### Containerization

#### LXC

-   [Lxc](Lxc.md "wikilink") - LXC Setup and Usage

#### Docker

-   [DockerOnUbuntu](DockerOnUbuntu.md "wikilink") - Docker on Ubuntu +
    Foreman Integration
-   [CentOS7Docker](CentOS7Docker.md "wikilink") - Install and configure
    Docker on CentOS7
-   [DockerFile](DockerFile.md "wikilink") - Example Dockerfile
-   [DockerCompose](DockerCompose.md "wikilink") - Example
    docker-compose.yml
-   [DockerSwarm](DockerSwarm.md "wikilink") - Docker Swarm Usage
-   [CleanUpDocker](CleanUpDocker.md "wikilink") - Clean up (delete) docker
    containers and images on local machine
-   [RemoveDockerCache](RemoveDockerCache.md "wikilink") - Prune Docker
    Cache

#### Kubernetes

-   [KubernetesClusterGoogleCloud](KubernetesClusterGoogleCloud.md "wikilink") -
    CI/CD example of a 4 container weather application using Google
    Container Register and Google Kubernetes Clusters
-   [MiniKube](MiniKube.md "wikilink") - MiniKube install and configure

#### OpenShift

-   [MiniShift](MiniShift.md "wikilink") - Minishift install and configure

### Virtualization / Hypervisor / Cloud

-   [VirtualBoxPassSMBIOS](VirtualBoxPassSMBIOS.md "wikilink") - Passing
    SMBios data to a Virtual Box guest to appear more hardware like
    (Mainly for Windows licensing on EFI machines)
-   [GoogleCloud](GoogleCloud.md "wikilink") - Quick setup on Google Cloud
-   [KVM+qemuCentOS6](KVM+qemuCentOS6.md "wikilink") - KVM notes for
    CentOS6

System Administration
---------------------

-   [SeleniumDocker](https://github.com/drew-holt/selenium-invadelabs) -
    GitHub: Selenium dockerized with Stand Alone Chrome and Firefox on
    separate ports.
-   [NagiosDocker](https://github.com/drew-holt/nagios-invadelabs) -
    GitHub: Invade Labs Nagios config using Docker
-   [ForceTextConsoleResolution](ForceTextConsoleResolution.md "wikilink") -
    Force text console resolution when using remote Lantronix Spider KVM
-   [LetsEncrypt](LetsEncrypt.md "wikilink") - letsencrypt.org config
-   [CustomKernelDebian](CustomKernelDebian.md "wikilink") - Compile a
    custom kernel from source in Debian / Ubuntu
-   [OctoPrint](OctoPrint.md "wikilink") - 3D printer interface
-   [XDripNightScout](XDripNightScout.md "wikilink") - Configuration for
    Dexcom G5, xDrip, xDripPebble, and NightScout
-   [Nmcli](Nmcli.md "wikilink") - Joining wifi from nmcli
-   [OpenVPN](OpenVPN.md "wikilink") - OpenVPN Server Setup
-   [ApachePAMunixAuth](ApachePAMunixAuth.md "wikilink") - Apache
    authentication against /etc/passwd
-   [Iptables](Iptables.md "wikilink") - iptables setup

##### Mail

-   [EmailViaNCorTelnet](EmailViaNCorTelnet.md "wikilink") - Send an email
    via nc or telnet
-   [SendmailRelayGmailCentos](SendmailRelayGmailCentos.md "wikilink") -
    Sendmail with gmail relay in Fedora 10+
-   [SendmailRelayISP](SendmailRelayISP.md "wikilink") - Sendmail using ISP
    as relay in Fedora 10+

##### DD-WRT

-   [Ddwrt-ddns-namecheap](Ddwrt-ddns-namecheap.md "wikilink") - Setup DDNS
    on DD-WRT for Namecheap
-   [PortMirroringDDWRTiptables](PortMirroringDDWRTiptables.md "wikilink") -
    Port mirroring with iptable in dd-wrt
-   [Ddwrtdnsmasq](Ddwrtdnsmasq.md "wikilink") - dnsmasq for DD-WRT
-   [PXEiSCSIboot](PXEiSCSIboot.md "wikilink") - Booting off SAN via PXE
    and iSCSI target
-   [Ddwrtopsware](Ddwrtopsware.md "wikilink") - opsware

##### File Server

-   [UbuntuRAID0ssd](UbuntuRAID0ssd.md "wikilink") -- Ubuntu RAID0 LVM SSD
    on root without boot partition
-   [NFS Optimization](NFS_Optimization.md "wikilink") - NFS Performance
    and Optimization
-   [Mdadm](Mdadm.md "wikilink") - Linux Software Raid Creation /
    Optimization
    -   [MdadmLVMext4](MdadmLVMext4.md "wikilink") - Best practices using
        md raid5 / LVM / ext4
    -   [BackupViaDDsnapshot](BackupViaDDsnapshot.md "wikilink") - Using
        LVM snapshotting to copy an LV
    -   [SmartdMonitoring](SmartdMonitoring.md "wikilink") - Monitor disks
        with smartmontools
    -   [USBhddtemp](USBhddtemp.md "wikilink") - Check hard drive temp for
        USB HD (Western Digital)
    -   [LoopBackSoftwareRaidMount](LoopBackSoftwareRaidMount.md "wikilink") -
        Imaging 2 of 3 RAID5 drives and loop back mounting for data
        extraction
-   [ResizePV](ResizePV.md "wikilink") - Steps to resize PV
-   [ECryptfs](ECryptfs.md "wikilink") - Private Encrypted Folders
-   [SambaTdbsamBackend](SambaTdbsamBackend.md "wikilink") - Using Samba
    Tdbsam backend with unix login

##### Backup

-   [BackupPartitionsViaDDandSfdisk](BackupPartitionsViaDDandSfdisk.md "wikilink") -
    Backup boot and system partitions with dd and sfdisk
-   [BackupDD-WRTConfig](BackupDD-WRTConfig.md "wikilink") - DD-WRT backup
    script (cron)
-   [ClamAVWeeklyScan](ClamAVWeeklyScan.md "wikilink") - ClamAV script
    (cron)
-   [MySQLBackupScript](MySQLBackupScript.md "wikilink") - MySQL Backup
    Script - (cron)
-   [RsyncSSHkeys](RsyncSSHkeys.md "wikilink") - Rsync over SSH - Different
    port / SSH Keys
-   [ExternalUSB+LUKS+LVM](ExternalUSB+LUKS+LVM.md "wikilink") - Encrypted
    LVM for External USB and LUKS for rsync backup

#### Hardware Related

-   [IPMI](IPMI.md "wikilink") - IPMI on SuperMicro AOC-IPMI20 with
    Serial-Over-LAN Console
-   [Lm\_sensorsPDMSi](Lm_sensorsPDMSi.md "wikilink") - lm\_sensors
    lmsensors /etc/sensors.d/pdsmi
-   [RaspberryPi](RaspberryPi.md "wikilink") - Information for RPi
-   [Udevinfo](Udevinfo.md "wikilink") - gathering system info
-   [Gps](Gps.md "wikilink") - GPS Related

Media
-----

-   [EGalaxyTouchScreen](EGalaxyTouchScreen.md "wikilink") - eGalaxy Touch
    Screen
-   [LinuxGPS](LinuxGPS.md "wikilink") - Linux GPS with sirfmon, gpsd, and
    more
-   [Independant X-server](Independant_X-server.md "wikilink") - Multi seat
    configuration for 2 seperate X servers on the same system
-   [LircConfig-MythTV+mplayer](LircConfig-MythTV+mplayer.md "wikilink")
-   [LircPinnacle800iComcastRemote](LircPinnacle800iComcastRemote.md "wikilink") -
    Remapping Comcast remote IR in ir-keymap.c kernel module
-   [CompizProfileConfiguration](CompizProfileConfiguration.md "wikilink") -
    Dual monitor / GiantCube / Ice Exploding Windows

Client Setup
------------

-   [Ubuntu17.10Setup](Ubuntu17.10Setup.md "wikilink") - Ubuntu 17.10
    workstation / laptop Setup
-   [MacOS](MacOS.md "wikilink") - macOS 10.14 MBP Mojave setup
-   [Windows10Setup](Windows10Setup.md "wikilink") - Windows 10 Laptop
    Setup
-   [RaspberryPISetup](RaspberryPISetup.md "wikilink") - RaspberryPi setup
    for drew-pi
-   [Pine64](Pine64.md "wikilink") - Pine64 Armbian Notes
-   [RikoAndroidMiniPC](RikoAndroidMiniPC.md "wikilink") - Rikomagic MK802
    III setup + picuntu

Outdated
--------

-   [ServerSetupFedora22](ServerSetupFedora22.md "wikilink") - Fedora 22
    Server Setup
-   [BootOptimization](BootOptimization.md "wikilink") - Speed up Fedora15
    boot
-   [NUTUPSMonitor](NUTUPSMonitor.md "wikilink") - Configure NUT for UPS
    monitoring and alerts in Fedora 12-14
-   [Fedora15Gnome3Tweaks](Fedora15Gnome3Tweaks.md "wikilink") - Fedora 15
    / GNOME3 Tweaks

Misc.
-----
