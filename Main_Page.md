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

-   [ServerSetupCentOS7](ServerSetupCentOS7 "wikilink") - CentOS7 Server
    setup with NFS/rsyslog/chrony/hw\_mon services + qemu+kvm libvirt +
    Puppet + Foreman + Docker
-   [ServerSetupFedora27](ServerSetupFedora27 "wikilink") - Fedora 27
    Server Setup

Infrastructure
--------------

### Infrastructure Automation

#### Chef

-   [InstallingChefServer](InstallingChefServer "wikilink") - Installing
    Chef Server
-   [KnifeBootstrapAWS](KnifeBootstrapAWS "wikilink") - knife
    bootstrapping AWS instances
-   [ChefEncryptedDataBags](ChefEncryptedDataBags "wikilink") - Creating
    and using encrypted data bags
-   [FoodcriticRubocop](FoodcriticRubocop "wikilink") - Linting recipes
    with Foodcritic and Rubocop
-   [TestingWithChefSpec](TestingWithChefSpec "wikilink") - Examples of
    using ChefSpec for unit and integration tests in cookbooks
-   [TestKitchenVagrant](TestKitchenVagrant "wikilink") - Test Kitchen
    with Vagrant provisioner for testing cookbooks
-   [TestKitchenDocker](TestKitchenDocker "wikilink") - Test Kitchen
    with Docker provisioner for testing cookbooks
-   [ChefJenkinsGroovyShellOut](ChefJenkinsGroovyShellOut "wikilink") -
    Shell out of recipe to use jenkins-cli to grab the encrypted or
    unencrytped value of a secret using Jenkins Groovy
-   [ChefMisc](ChefMisc "wikilink") - Misc Chef

#### Puppet

-   [MultiMachineVagrantPuppetJenkinsNexus](MultiMachineVagrantPuppetJenkinsNexus "wikilink") -
    Multimachine Vagrant boxes with 1 Puppet Server, 1 Puppet Client,
    and 1 Jenkins/Nexus VM to deploy Tomcat via Puppet

#### Ansible

-   [AnsibleVirtualboxDocker](https://github.com/drew-holt/ansible-invadelabs) -
    GitHub: Invade Labs test environment for Ansible with VirtualBox VMs
    running Docker in a dind cluster

#### Terraform

-   [TerraformExamples](TerraformExamples "wikilink") - Terraform
    examples placeholder

#### Jenkins

-   [DisableJenkins2Wizard](DisableJenkins2Wizard "wikilink") - Disable
    Jenkins 2.0 Setup Wizard
-   [JenkinsSecurityViaDSL](JenkinsSecurityViaDSL "wikilink") - Jenkins
    Security via DSL
-   [ListJenkinsPluginsViaCurl](ListJenkinsPluginsViaCurl "wikilink") -
    List Jenkins plugins via curl

### Containerization

#### LXC

-   [Lxc](Lxc "wikilink") - LXC Setup and Usage

#### Docker

-   [DockerOnUbuntu](DockerOnUbuntu "wikilink") - Docker on Ubuntu +
    Foreman Integration
-   [CentOS7Docker](CentOS7Docker "wikilink") - Install and configure
    Docker on CentOS7
-   [DockerFile](DockerFile "wikilink") - Example Dockerfile
-   [DockerCompose](DockerCompose "wikilink") - Example
    docker-compose.yml
-   [DockerSwarm](DockerSwarm "wikilink") - Docker Swarm Usage
-   [CleanUpDocker](CleanUpDocker "wikilink") - Clean up (delete) docker
    containers and images on local machine
-   [RemoveDockerCache](RemoveDockerCache "wikilink") - Prune Docker
    Cache

#### Kubernetes

-   [KubernetesClusterGoogleCloud](KubernetesClusterGoogleCloud "wikilink") -
    CI/CD example of a 4 container weather application using Google
    Container Register and Google Kubernetes Clusters
-   [MiniKube](MiniKube "wikilink") - MiniKube install and configure

#### OpenShift

-   [MiniShift](MiniShift "wikilink") - Minishift install and configure

### Virtualization / Hypervisor / Cloud

-   [VirtualBoxPassSMBIOS](VirtualBoxPassSMBIOS "wikilink") - Passing
    SMBios data to a Virtual Box guest to appear more hardware like
    (Mainly for Windows licensing on EFI machines)
-   [GoogleCloud](GoogleCloud "wikilink") - Quick setup on Google Cloud
-   [KVM+qemuCentOS6](KVM+qemuCentOS6 "wikilink") - KVM notes for
    CentOS6

System Administration
---------------------

-   [SeleniumDocker](https://github.com/drew-holt/selenium-invadelabs) -
    GitHub: Selenium dockerized with Stand Alone Chrome and Firefox on
    separate ports.
-   [NagiosDocker](https://github.com/drew-holt/nagios-invadelabs) -
    GitHub: Invade Labs Nagios config using Docker
-   [ForceTextConsoleResolution](ForceTextConsoleResolution "wikilink") -
    Force text console resolution when using remote Lantronix Spider KVM
-   [LetsEncrypt](LetsEncrypt "wikilink") - letsencrypt.org config
-   [CustomKernelDebian](CustomKernelDebian "wikilink") - Compile a
    custom kernel from source in Debian / Ubuntu
-   [OctoPrint](OctoPrint "wikilink") - 3D printer interface
-   [XDripNightScout](XDripNightScout "wikilink") - Configuration for
    Dexcom G5, xDrip, xDripPebble, and NightScout
-   [Nmcli](Nmcli "wikilink") - Joining wifi from nmcli
-   [OpenVPN](OpenVPN "wikilink") - OpenVPN Server Setup
-   [ApachePAMunixAuth](ApachePAMunixAuth "wikilink") - Apache
    authentication against /etc/passwd
-   [Iptables](Iptables "wikilink") - iptables setup

##### Mail

-   [EmailViaNCorTelnet](EmailViaNCorTelnet "wikilink") - Send an email
    via nc or telnet
-   [SendmailRelayGmailCentos](SendmailRelayGmailCentos "wikilink") -
    Sendmail with gmail relay in Fedora 10+
-   [SendmailRelayISP](SendmailRelayISP "wikilink") - Sendmail using ISP
    as relay in Fedora 10+

##### DD-WRT

-   [Ddwrt-ddns-namecheap](Ddwrt-ddns-namecheap "wikilink") - Setup DDNS
    on DD-WRT for Namecheap
-   [PortMirroringDDWRTiptables](PortMirroringDDWRTiptables "wikilink") -
    Port mirroring with iptable in dd-wrt
-   [Ddwrtdnsmasq](Ddwrtdnsmasq "wikilink") - dnsmasq for DD-WRT
-   [PXEiSCSIboot](PXEiSCSIboot "wikilink") - Booting off SAN via PXE
    and iSCSI target
-   [Ddwrtopsware](Ddwrtopsware "wikilink") - opsware

##### File Server

-   [UbuntuRAID0ssd](UbuntuRAID0ssd "wikilink") -- Ubuntu RAID0 LVM SSD
    on root without boot partition
-   [NFS Optimization](NFS_Optimization "wikilink") - NFS Performance
    and Optimization
-   [Mdadm](Mdadm "wikilink") - Linux Software Raid Creation /
    Optimization
    -   [MdadmLVMext4](MdadmLVMext4 "wikilink") - Best practices using
        md raid5 / LVM / ext4
    -   [BackupViaDDsnapshot](BackupViaDDsnapshot "wikilink") - Using
        LVM snapshotting to copy an LV
    -   [SmartdMonitoring](SmartdMonitoring "wikilink") - Monitor disks
        with smartmontools
    -   [USBhddtemp](USBhddtemp "wikilink") - Check hard drive temp for
        USB HD (Western Digital)
    -   [LoopBackSoftwareRaidMount](LoopBackSoftwareRaidMount "wikilink") -
        Imaging 2 of 3 RAID5 drives and loop back mounting for data
        extraction
-   [ResizePV](ResizePV "wikilink") - Steps to resize PV
-   [ECryptfs](ECryptfs "wikilink") - Private Encrypted Folders
-   [SambaTdbsamBackend](SambaTdbsamBackend "wikilink") - Using Samba
    Tdbsam backend with unix login

##### Backup

-   [BackupPartitionsViaDDandSfdisk](BackupPartitionsViaDDandSfdisk "wikilink") -
    Backup boot and system partitions with dd and sfdisk
-   [BackupDD-WRTConfig](BackupDD-WRTConfig "wikilink") - DD-WRT backup
    script (cron)
-   [ClamAVWeeklyScan](ClamAVWeeklyScan "wikilink") - ClamAV script
    (cron)
-   [MySQLBackupScript](MySQLBackupScript "wikilink") - MySQL Backup
    Script - (cron)
-   [RsyncSSHkeys](RsyncSSHkeys "wikilink") - Rsync over SSH - Different
    port / SSH Keys
-   [ExternalUSBEncryptedLVM](ExternalUSBEncryptedLVM "wikilink") -
    Encrypted LVM for External USB (rsync backup)

#### Hardware Related

-   [IPMI](IPMI "wikilink") - IPMI on SuperMicro AOC-IPMI20 with
    Serial-Over-LAN Console
-   [Lm\_sensorsPDMSi](Lm_sensorsPDMSi "wikilink") - lm\_sensors
    lmsensors /etc/sensors.d/pdsmi
-   [RaspberryPi](RaspberryPi "wikilink") - Information for RPi
-   [Udevinfo](Udevinfo "wikilink") - gathering system info
-   [Gps](Gps "wikilink") - GPS Related

Media
-----

-   [EGalaxyTouchScreen](EGalaxyTouchScreen "wikilink") - eGalaxy Touch
    Screen
-   [LinuxGPS](LinuxGPS "wikilink") - Linux GPS with sirfmon, gpsd, and
    more
-   [Independant X-server](Independant_X-server "wikilink") - Multi seat
    configuration for 2 seperate X servers on the same system
-   [LircConfig-MythTV+mplayer](LircConfig-MythTV+mplayer "wikilink")
-   [LircPinnacle800iComcastRemote](LircPinnacle800iComcastRemote "wikilink") -
    Remapping Comcast remote IR in ir-keymap.c kernel module
-   [CompizProfileConfiguration](CompizProfileConfiguration "wikilink") -
    Dual monitor / GiantCube / Ice Exploding Windows

Client Setup
------------

-   [Ubuntu17.10Setup](Ubuntu17.10Setup "wikilink") - Ubuntu 17.10
    workstation / laptop Setup
-   [MacOS](MacOS "wikilink") - macOS 10.14 MBP Mojave setup
-   [Windows10Setup](Windows10Setup "wikilink") - Windows 10 Laptop
    Setup
-   [RaspberryPISetup](RaspberryPISetup "wikilink") - RaspberryPi setup
    for drew-pi
-   [Pine64](Pine64 "wikilink") - Pine64 Armbian Notes
-   [RikoAndroidMiniPC](RikoAndroidMiniPC "wikilink") - Rikomagic MK802
    III setup + picuntu

Outdated
--------

-   [ServerSetupFedora22](ServerSetupFedora22 "wikilink") - Fedora 22
    Server Setup
-   [BootOptimization](BootOptimization "wikilink") - Speed up Fedora15
    boot
-   [NUTUPSMonitor](NUTUPSMonitor "wikilink") - Configure NUT for UPS
    monitoring and alerts in Fedora 12-14
-   [Fedora15Gnome3Tweaks](Fedora15Gnome3Tweaks "wikilink") - Fedora 15
    / GNOME3 Tweaks

Misc.
-----
