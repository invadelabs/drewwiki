---
title: Main Page
layout: default
---

A collection of randomness I've encountered and configured in Linux.

System Setup
------------

-   [ServerSetupCentOS7](ServerSetupCentOS7 "wikilink") - CentOS7 Server
    setup with NFS/rsyslog/chrony/hw\_mon services + qemu+kvm libvirt +
    Foreman + Docker
-   [ServerSetupFedora22](ServerSetupFedora22 "wikilink") - Fedora 22
    Server Setup

Infrastructure Automation
-------------------------

### Chef

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

### Puppet

-   [MultiMachineVagrantPuppetJenkinsNexus](MultiMachineVagrantPuppetJenkinsNexus "wikilink") -
    Multimachine Vagrant boxes with 1 Pupper Server, 1 Puppet Client,
    and 1 Jenkins/Nexus VM to deploy Tomcat via Puppet

### Ansible

[1](https://github.com/drew-holt/ansible-invadelabs) - Invade Labs test
environment for Ansible and VirtualBox on GitHub

### Docker

[CentOS7Docker](CentOS7Docker "wikilink") - Install and configure Docker
on CentOS7 [DockerFile](DockerFile "wikilink") - Example Dockerfile
[DockerCompose](DockerCompose "wikilink") - Example docker-compose.yml
[DockerSwarm](DockerSwarm "wikilink") - Docker Swarm Usage
[CleanUpDocker](CleanUpDocker "wikilink") - Clean up (delete) docker
containers and images on local machine
[RemoveDockerCache](RemoveDockerCache "wikilink") - Prune Docker Cache

System Administration
---------------------

-   [VirtualBoxPassSMBIOS](VirtualBoxPassSMBIOS "wikilink") - Passing
    SMBios data to a Virtual Box guest to appear more hardware like
    (Mainly for Windows licensing on EFI machines)
-   [EmailViaNCorTelnet](EmailViaNCorTelnet "wikilink") - Send an email
    via nc or telnet
-   [GoogleCloud](GoogleCloud "wikilink") - Quick setup on Google Cloud
-   [DockerOnUbuntu](DockerOnUbuntu "wikilink") - Docker on Ubuntu +
    Foreman Integration
-   [LetsEncrypt](LetsEncrypt "wikilink") - letsencrypt.org config
-   [backuppartitionsddandsfdisk](backuppartitionsddandsfdisk "wikilink") -
    Backup boot and system partitions with dd and sfdisk
-   [KVM/qemu CentOS6](KVM/qemu_CentOS6 "wikilink") - KVM notes for
    CentOS6
-   [lxc](lxc "wikilink") - LXC Setup and Usage(Linux Containers)
-   [CustomKernelDebian](CustomKernelDebian "wikilink") - Compile a
    custom kernel from source in Debian / Ubuntu
-   [OctoPrint](OctoPrint "wikilink") - 3D printer interface
-   [xDripNightScout](xDripNightScout "wikilink") - Configuration for
    Dexcom G5, xDrip, xDripPebble, and NightScout
-   [nmcli](nmcli "wikilink") - Joining wifi from nmcli
-   [ddwrt-ddns-namecheap](ddwrt-ddns-namecheap "wikilink") - Setup DDNS
    on DD-WRT for Namecheap
-   [OpenVPN](OpenVPN "wikilink") - OpenVPN Server Setup
-   [ApachePAMunixAuth](ApachePAMunixAuth "wikilink") - Apache
    authentication against /etc/passwd
-   [SendmailRelayGmailCentos](SendmailRelayGmailCentos "wikilink") -
    Sendmail with gmail relay in Fedora 10+
-   [SendmailRelayISP](SendmailRelayISP "wikilink") - Sendmail using ISP
    as relay in Fedora 10+
-   [IPMI](IPMI "wikilink") - IPMI on SuperMicro AOC-IPMI20 with
    Serial-Over-LAN Console
-   lm\_sensors
    -   [lm\_sensorsPDMSi](lm_sensorsPDMSi "wikilink") -
        /etc/sensors.d/pdsmi
-   [iptables](iptables "wikilink") - iptables setup
-   DD-WRT - all things dd-wwrt
    -   [ddwrtdnsmasq](ddwrtdnsmasq "wikilink") - dnsmasq for DD-WRT
    -   [PXEiSCSIboot](PXEiSCSIboot "wikilink") - Booting off SAN via
        PXE and iSCSI target
    -   [ddwrtopsware](ddwrtopsware "wikilink") - opsware
-   [PortMirroringDDWRTiptables](PortMirroringDDWRTiptables "wikilink") -
    Port mirroring with iptable in dd-wrt

##### File Server

-   [NFS Optimization](NFS_Optimization "wikilink") - NFS Performance
    and Optimization
-   [mdadm](mdadm "wikilink") - Linux Software Raid Creation /
    Optimization
    -   [mdadmLVMext4](mdadmLVMext4 "wikilink") - Best practices using
        md raid5 / LVM / ext4
    -   [BackupViaDDsnapshot](BackupViaDDsnapshot "wikilink") - Using
        LVM snapshotting to copy an LV
    -   [smartdMonitoring](smartdMonitoring "wikilink") - Monitor disks
        with smartmontools
    -   [USBhddtemp](USBhddtemp "wikilink") - Check hard drive temp for
        USB HD (Western Digital)
    -   [LoopBackSoftwareRaidMount](LoopBackSoftwareRaidMount "wikilink") -
        Imaging 2 of 3 RAID5 drives and loop back mounting for data
        extraction
-   [ResizePV](ResizePV "wikilink") - Steps to resize PV
-   [eCryptfs](eCryptfs "wikilink") - Private Encrypted Folders
-   [SambaTdbsamBackend](SambaTdbsamBackend "wikilink") - Using Samba
    Tdbsam backend with unix login

##### Backup

-   [Backup DD-WRT Config](Backup_DD-WRT_Config "wikilink") - DD-WRT
    backup script (cron)
-   [ClamAV Weekly Scan](ClamAV_Weekly_Scan "wikilink") - ClamAV script
    (cron)
-   [MySQL Backup Script](MySQL_Backup_Script "wikilink") - MySQL Backup
    Script - (cron)
-   [rsyncSSHkeys](rsyncSSHkeys "wikilink") - Rsync over SSH - Different
    port / SSH Keys
-   [ExternalUSBEncryptedLVM](ExternalUSBEncryptedLVM "wikilink") -
    Encrypted LVM for External USB (rsync backup)

#### Hardware Related

-   [RaspberryPi](RaspberryPi "wikilink") - Information for RPi
-   [udevinfo](udevinfo "wikilink") - gathering system info
-   [gps](gps "wikilink") - GPS Related
-   ssd - Solid State Drive articles
    -   [UbuntuRAID0ssd](UbuntuRAID0ssd "wikilink") -- Ubuntu RAID0 LVM
        on SSD on root no boot partition

Media
-----

-   [eGalaxyTouchScreen](eGalaxyTouchScreen "wikilink") - eGalaxy Touch
    Screen
-   [LinuxGPS](LinuxGPS "wikilink") - Linux GPS with sirfmon, gpsd, and
    more
-   [mencoder](mencoder "wikilink") - codecs(x264, lavc, xvid) /
    de-interlace filters / dvd
-   [mplayer](mplayer "wikilink") - dvd and dvb playback / xvmc and
    vdpau gpu decoder offload
-   [Independant X-server](Independant_X-server "wikilink") - Multi seat
    configuration for 2 seperate X servers on the same system
-   [Lirc Config - MythTV /
    mplayer](Lirc_Config_-_MythTV_/_mplayer "wikilink")
-   [Lirc, Pinnacle 800i, and Comcast
    Remote](Lirc,_Pinnacle_800i,_and_Comcast_Remote "wikilink") -
    Remapping Comcast remote IR in ir-keymap.c kernel module
-   [ConvertVideoToM4a](ConvertVideoToM4a "wikilink") - Convert video to
    m4a with ffmpeg copy
-   [bluray](bluray "wikilink") - Playing and backing up Blu-ray discs
    in Linux

#### Window Manager Related

-   [Compiz Profile
    Configuration](Compiz_Profile_Configuration "wikilink") - Dual
    monitor / GiantCube / Ice Exploding Windows
-   TomBoy notes - WebDav Sync

#### Emulators

-   [N64Mupen64plus](N64Mupen64plus "wikilink") - Using mupen64plus (N64
    Emulator) in Linux

Client Setup
------------

-   [DesktopSetup](DesktopSetup "wikilink") - Ubuntu 17.10 setup for
    drew-itx
-   [Ubuntu 17.10 Setup](Ubuntu_17.10_Setup "wikilink") - Ubuntu 17.10
    Setup for laptop
-   [OSX Setup](OSX_Setup "wikilink") - macOS 10.11 MBP Sierra setup
-   [RaspberryPISetup](RaspberryPISetup "wikilink") - RaspberryPi setup
    for drew-pi
-   [Pine64](Pine64 "wikilink") - Pine64 Armbian Notes
-   [RikoAndroidMiniPC](RikoAndroidMiniPC "wikilink") - Rikomagic MK802
    III setup + picuntu
-   [Windows Setup](Windows_Setup "wikilink") - Windows 8 / Windows 10
    Setup
-   [ChromebookSetup](ChromebookSetup "wikilink") - Chromebook Setup

Outdated
--------

-   [BootOptimization](BootOptimization "wikilink") - Speed up Fedora15
    boot
-   [NUTUPSMonitor](NUTUPSMonitor "wikilink") - Configure NUT for UPS
    monitoring and alerts in Fedora 12-14
-   [Fedora15Gnome3Tweaks](Fedora15Gnome3Tweaks "wikilink") - Fedora 15
    / GNOME3 Tweaks

Misc.
-----
