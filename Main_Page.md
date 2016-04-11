---
title: Main Page
layout: default
---

A collection of randomness I've encountered and configured in Linux. -
drewderivative@gmail.com

System Setup
------------

-   [MultiMachineVagrantPuppetJenkinsNexus](MultiMachineVagrantPuppetJenkinsNexus "wikilink") -
    Setting up a multi machine vagrant with 1 Pupper Server, 1 Puppet
    Client, and 1 Jenkins/Nexus VM
-   [ServerSetupCentOS7](ServerSetupCentOS7 "wikilink") - New Server
    setup for drewserv with CentOS7 + NFS/rsyslog/chrony/hw\_mon
    services + qemu+kvm libvirt + Foreman
-   [ServerSetupFedora22](ServerSetupFedora22 "wikilink") - OLD Server
    setup for drewserv
-   [DesktopSetup](DesktopSetup "wikilink") - Desktop setup for
    drew-desktop
-   [RaspberryPISetup](RaspberryPISetup "wikilink") - RaspberryPi setup
    for drewpi
-   [RikoAndroidMiniPC](RikoAndroidMiniPC "wikilink") - Rikomagic MK802
    III setup + picuntu
-   [OSX Setup](OSX_Setup "wikilink") - Laptop software config
-   [ChromebookSetup](ChromebookSetup "wikilink") - Chromebook Setup
-   [Windows Setup](Windows_Setup "wikilink") - Windows 8 / Windows 10
    Setup

System Administration
---------------------

-   [xDripNightScout](xDripNightScout "wikilink") - Configuration for
    Dexcom G5, xDrip, xDripPebble, and NightScout
-   [DockerOnUbuntu](DockerOnUbuntu "wikilink") - Docker on Ubuntu +
    Foreman Integration
-   [LetsEncrypt](LetsEncrypt "wikilink") - letsencrypt.org config
-   [backuppartitionsddandsfdisk](backuppartitionsddandsfdisk "wikilink") -
    Backup boot and system partitions with dd and sfdisk
-   [KVM/qemu CentOS6](KVM/qemu_CentOS6 "wikilink") - KVM notes
-   [nmcli](nmcli "wikilink") - Joining wifi from nmcli
-   [lxc](lxc "wikilink") - LXC (Linux Containers)
-   [ddwrt-ddns-namecheap](ddwrt-ddns-namecheap "wikilink") - Setup DDNS
    on DD-WRT for Namecheap
-   [CustomKernelDebian](CustomKernelDebian "wikilink") - Compile a
    custom kernel from source in Debian / Ubuntu
-   [OpenVPN](OpenVPN "wikilink") - OpenVPN Server Setup
-   [MirrorWikipedia](MirrorWikipedia "wikilink") - Attempts to mirror
    wikipedia.org dumps
-   [BootOptimization](BootOptimization "wikilink") - Speed up F15 boot
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
-   DD-WRT
    -   [ddwrtdnsmasq](ddwrtdnsmasq "wikilink") - dnsmasq stuff for
        DD-WRT
    -   [PXEiSCSIboot](PXEiSCSIboot "wikilink") - Booting off SAN via
        PXE and iSCSI target
    -   [ddwrtopsware](ddwrtopsware "wikilink") - opsware
-   [NUTUPSMonitor](NUTUPSMonitor "wikilink") - Configure NUT for UPS
    monitoring and alerts in Fedora 12-14
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
-   [SambaTdbsamBackend](SambaTdbsamBackend "wikilink")
-   SELinux

##### Backup

-   [Backup DD-WRT Config](Backup_DD-WRT_Config "wikilink") (cron)
-   [ClamAV Weekly Scan](ClamAV_Weekly_Scan "wikilink") (cron)
-   [MySQL Backup Script](MySQL_Backup_Script "wikilink") (cron)
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
-   [Independant X-server](Independant_X-server "wikilink")
-   [Lirc Config - MythTV /
    mplayer](Lirc_Config_-_MythTV_/_mplayer "wikilink")
-   [Lirc, Pinnacle 800i, and Comcast
    Remote](Lirc,_Pinnacle_800i,_and_Comcast_Remote "wikilink") -
    ir-keymap.c
-   [ConvertVideoToM4a](ConvertVideoToM4a "wikilink") - Convert video to
    m4a with ffmpeg copy
-   [bluray](bluray "wikilink") - Playing and backing up Blu-ray discs
    in Linux

#### Window Manager Related

-   [Compiz Profile
    Configuration](Compiz_Profile_Configuration "wikilink") - (Dual
    monitor/GiantCube/IceExploding Windows)
-   [Fedora15Gnome3Tweaks](Fedora15Gnome3Tweaks "wikilink") - Fedora 15
    / GNOME3 Tweaks
-   TomBoy notes - WebDav Sync

#### Emulators

-   [N64Mupen64plus](N64Mupen64plus "wikilink") - Using mupen64plus (N64
    Emulator) in Linux

Misc.
-----

-   [PowerDraw](PowerDraw "wikilink")
-   [Research](Research "wikilink")

