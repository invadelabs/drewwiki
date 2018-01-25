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

Show username in Desktop Manager
--------------------------------

``` bash
gsettings set com.canonical.indicator.session show-real-name-on-panel true
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

    TopIcons-plus - for insync prime, slack
    Extension update notifier
    Freon
    Status area horizontal spacing
    $ ~/.local/share/gnome-shell/extensions
    sudo apt-get install chrome-gnome-shell
    * restart GNOME Shell (Alt+F2, r, Enter) and enable the extension through gnome-tweak-tool.

Install Main Apps
=================

``` bash
sudo apt-get install \
keepass2 rdesktop vncviewer \
lm-sensors p7zip-full exfat-utils exfat-fuse \
vim ssh git \
ubuntu-restricted-extras qbittorrent gimp audacity \ 
icedtea-8-plugin \
network-manager-openvpn wireshark  nmap \
openvpn openssh-server fail2ban \
vlc vlc-plugin-fluidsynth ffmpeg atomicparsley \
chrome-gnome-shell \
gnome-tweaks

** Atom
** sqlitebrowser
** VirtualBox
** Vagrant
** vagrant plugin install vagrant-berkshelf
** vagrant plugin install berkshelf
** Docker
** Chrome, verify Google Hangouts
** Insynq
** Synergy
** Ramlog or equivalent for SSD
** nvm
** rvm
** Studio 3T (mongodb browswer)
** IntelliJ
** Android Studio
** Eclipse
** NetBeans
** PyCharm

drew@drew-8570w:~$ snap list
Name                  Version                  Rev   Developer      Notes
atom                  1.23.1                   109   snapcrafters   classic
core                  16-2.29.4.2              3604  canonical      core
cumulonimbus          1.6.7                    18    snapcrafters   -
drive                 current                  22    fireeye        -
gitter-desktop        3.1.0                    20    snapcrafters   -
go                    1.9.2                    1016  mwhudson       classic
jenkins               2.8                      6     snapcrafters   -
juju                  2.3.1                    3106  canonical      classic
kubectl               1.9.0                    266   canonical      classic
lxd                   2.21                     5408  canonical      -
mongo33               3.3.9                    2     niemeyer       -
openhab               2.0.0                    167   openhab        -
picard                1.4.2                    2     pachulo        -
pycharm-professional  2017.3.2                 46    jetbrains      classic
spotify               1.0.70.399.g5ffabd56-26  5     spotify        -
sqlitebrowser-casept  3.9.1                    2     casept         -
vault                 v0.9.0                   236   snapcrafters   -
vscode                1.19.1-1513676564        22    flexiondotorg  classic


oracle-java8-installer
cairo-dock
adobe-flashplugin
encfs youtube-dl nikto exiftool chkrootkit apache2-utils pidgin wavemon xd docker.io virtualenv python2.7-examples mailutils ansible namebench python-pip (via apt)
xchat
youtube-dl
```

Other
=====

``` bash
sudo apt-get install -y nfs-common cifs-utils ethtool pm-utils
```

Other Configuration
===================

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
