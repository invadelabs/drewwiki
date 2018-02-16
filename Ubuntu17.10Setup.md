---
title: Ubuntu17.10Setup
layout: default
---

After initial install
=====================

``` bash
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get dist-upgrade

sudo apt-get install -y etckeeper
cd /etc
sudo etckeeper init
sudo vi .gitignore # remove sensitive files
```

Disable Guest Login
-------------------

``` bash
sudo sh -c "echo 'allow-guest=false' >> /usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf"
```

Set vim Editor
--------------

``` bash
sudo update-alternatives --set editor /usr/bin/vim.basic
```

Set passwordless sudo
---------------------

``` bash
visudo:
username ALL=(ALL) NOPASSWD: ALL
```

Dash to Dock
------------

<https://extensions.gnome.org/extension/307/dash-to-dock/>

Set gnome-screenshot default save directory
-------------------------------------------

?

Gnome3 Fix alt+tab to move across widnows and not just grouped apps
-------------------------------------------------------------------

``` bash
Open dconf-editor
Go to org/gnome/desktop/wm/keybindings
Move the value '<Alt>Tab' from switch-applications to switch-windows
Optionally move '<Shift><Alt>Tab' from switch-applications-backward to switch-windows-backward
If you want switch-windows to work across desktops, not just in the current desktop, you can also uncheck org/gnome/shell/window-switcher/current-workspace-only (Courtesy of @CharlBotha)
Close dconf-editor
Press <Alt>F2, then type r to restart Gnome.
```

[1](https://superuser.com/questions/394376/how-to-prevent-gnome-shells-alttab-from-grouping-windows-from-similar-apps)

Gnome Tweak Tool
----------------

``` bash
TopIcons-plus - for Insync, Slack, Skype icons
Extension update notifier
Freon
Status area horizontal spacing
$ ~/.local/share/gnome-shell/extensions
sudo apt-get install chrome-gnome-shell
* restart GNOME Shell (Alt+F2, r, Enter) and enable the extension through gnome-tweak-tool.
```

Install Main Apps
=================

``` bash
sudo apt-get install \
keepass2 rdesktop vncviewer \
lm-sensors p7zip-full exfat-utils exfat-fuse encfs \
vim ssh git \
ubuntu-restricted-extras qbittorrent gimp audacity \ 
openjdk-8-jre icedtea-8-plugin oracle-java8-installer \
network-manager-openvpn wireshark nmap nikto chkrootkit wavemon namebench apache2-utils mailutils \
openvpn openssh-server fail2ban \
vlc vlc-plugin-fluidsynth ffmpeg atomicparsley \
virtualenv python2.7-examples python-pip \
xchat pidgin \
chrome-gnome-shell \
ansible \
gnome-tweaks

#xd exiftol
```

-   -   Atom [2](https://atom.io/)
    -   sqlitebrowser
    -   youtube-dl (via pip)
    -   VirtualBox [3](https://www.virtualbox.org/)
    -   Vagrant [4](https://www.vagrantup.com/)
        -   vagrant plugin install vagrant-berkshelf
        -   vagrant plugin install berkshelf
    -   Terraform [5](https://www.terraform.io/)
    -   Docker
        [6](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
    -   Chrome, verify Google Hangouts
    -   Insynq [7](https://www.insynchq.com/downloads)
    -   Synergy
    -   Ramlog or equivalent for SSD
    -   nvm
    -   gvm for goland
    -   rvm [Ubuntu RVM Instructions](https://github.com/rvm/ubuntu_rvm)
    -   Studio 3T (mongodb browswer) (https://studio3t.com/download/)
    -   IntelliJ [8](https://www.jetbrains.com/idea/download/)
    -   Android Studio
        [9](https://developer.android.com/studio/index.html)
    -   Eclipse [10](https://www.eclipse.org/)
    -   NetBeans [11](https://netbeans.org/downloads/)
    -   PyCharm
        [12](https://www.jetbrains.com/pycharm/download/#section=linux)

``` bash
drew@drew-8570w:~$ snap list
Name                  Version                  Rev   Developer      Notes
core                  16-2.29.4.2              3604  canonical      core
cumulonimbus          1.6.7                    18    snapcrafters   -
drive                 current                  22    fireeye        -
gitter-desktop        3.1.0                    20    snapcrafters   -
juju                  2.3.1                    3106  canonical      classic
kubectl               1.9.0                    266   canonical      classic
picard                1.4.2                    2     pachulo        -
spotify               1.0.70.399.g5ffabd56-26  5     spotify        -
sqlitebrowser-casept  3.9.1                    2     casept         -
vault                 v0.9.0                   236   snapcrafters   -
vscode                1.19.1-1513676564        22    flexiondotorg  classic
```

Other NFS
=========

``` bash
sudo apt-get install -y nfs-common cifs-utils ethtool pm-utils
```

Other Syslog
============

Remote syslog

``` bash
echo "*.* @192.168.1.200" >> /etc/rsyslog.d/50-default.conf
```

-   tmpfs for /tmp and (maybe make this a bind mount..)

``` bash
tmpfs   /tmp       tmpfs   defaults,noatime,mode=1777   0  0
```

-   /etc/fstab

``` bash
192.168.1.200:/mnt/raid5 /mnt/raid5 nfs defaults    0 0
```

-   web server if needed

``` bash
sudo apt-get install apache2 php5 php5-sqlite
```
