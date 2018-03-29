---
title: Ubuntu17.10Setup
layout: default
---

Install Main Apps
=================

``` bash
#!/bin/bash
# set github
git config --global user.name "Drew Holt"
git config --global user.email "drewderivative@gmail.com"

# add me to sudoers
sudo sh -c 'echo "drew ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'

# remove clutter
cd $HOME; rmdir Documents/ Music/ Public/ Templates/ Videos/; rm examples.desktop

# local installers already gathered
sudo mkdir /mnt/hdd
sudo mount /dev/vg_hdd/lv_hdd /mnt/hdd
cd /mnt/hdd/iso_installers/ubuntu-installers
sudo apt-get install -y ./atom-amd64.deb ./google-chrome-stable_current_amd64.deb ./insync_1.4.4.37065-artful_amd64.deb ./slack-desktop-3.1.0-amd64.deb ./vagrant_2.0.3_x86_64.deb ./virtualbox-5.2_5.2.8-121009_Ubuntu_zesty_amd64.deb ./skypeforlinux-64.deb ./keybase_amd64.deb

## disable popularity-contest
#sudo dpkg-reconfigure popularity-contest # disable

# docker add repo
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
# oracle 8 add java repo
sudo add-apt-repository -y ppa:webupd8team/java

# update all repos, upgrade
sudo apt-get update
sudo apt-get -y dist-upgrade

# install etckeeper and initialize it
sudo apt-get install -y etckeeper
sudo etckeeper init

# Oracle Java 8 License
echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections

# install all the software
DEBIAN_FRONTEND=noninteractive `#no prompting` \
sudo apt-get install -y \
keepass2 synergy gnome-tweak-tool chrome-gnome-shell `#tools` \
vim vim-scripts vim-runtime vim-doc curl xd \
lm-sensors p7zip-full exfat-utils exfat-fuse encfs libimage-exiftool-perl `#systools` \
ubuntu-restricted-extras gimp audacity vlc vlc-plugin-fluidsynth ffmpeg atomicparsley `#media` \
openjdk-8-jdk icedtea-8-plugin `#java` \
openssh-server fail2ban `#daemon` \
openvpn network-manager-openconnect-gnome network-manager-openvpn-gnome `#network-client` \
rdesktop freerdp2-x11 xtightvncviewer sshpass qbittorrent wireshark nmap nikto chkrootkit wavemon namebench apache2-utils mailutils `#netutils` \
virtualenv python2.7-examples python-pip `#python` \
build-essential `#build-tools` \
sqlitebrowser yamllint highlight gawk `#dev-tools` \
lynis pandoc apt-transport-https `#misc` \
xchat pidgin `#chatapps` \
docker-ce `#docker` \
oracle-java8-installer `#oraclejava8` \
ansible `#automation`

# Set good vim
sudo update-alternatives --set editor /usr/bin/vim.basic

# install youtube-dl
pip install youtube-dl

# set env and aliases
cat <<EOF >> $HOME/.bashrc
export PATH="$HOME/.local/bin:$PATH"
alias xclip='xclip -selection clipboard'
alias rdesktop='rdesktop -g 1280x720 -r clipboard:CLIPBOARD -r disk:share=/home/drew'
alias get_ip='_get_ip() { VBoxManage guestproperty get "$1" "/VirtualBox/GuestInfo/Net/1/V4/IP";}; _get_ip'
EOF

# docker
sudo usermod -a -G docker drew
```

-   Chrome [1](https://www.google.com/chrome/)

<!-- -->

-   Atom [2](https://atom.io/)

``` bash
apm install atom-beautify linter-flake8 linter-pep8 autocomplete-python django-templates script-runner teletype
```

-   VirtualBox [3](https://www.virtualbox.org/)

``` bash
echo y | sudo VBoxManage extpack install "Oracle_VM_VirtualBox_Extension_Pack-5.2.8.vbox-extpack"
```

-   Vagrant [4](https://www.vagrantup.com/)

``` bash
vagrant plugin install vagrant-berkshelf; vagrant plugin install berkshelf
```

-   KeyBase [5](https://keybase.io)

``` bash
run_keybase
```

-   Insynq [6](https://www.insynchq.com/downloads)

``` bash
insync start ### do some magic here so we don't have to resync 200GB of google drive
```

-   Slack [7](https://slack.com/downloads/linux)

<!-- -->

-   Skype [8](https://www.skype.com/en/get-skype/skype-for-linux/)

Next
====

-   Terraform [9](https://www.terraform.io/)
-   Gitter
-   Ramlog or equivalent for SSD
-   nvm
-   gvm for goland
-   rvm [Ubuntu RVM Instructions](https://github.com/rvm/ubuntu_rvm)
-   Studio 3T (mongodb browswer) (https://studio3t.com/download/)
-   IntelliJ [10](https://www.jetbrains.com/idea/download/)
-   Android Studio [11](https://developer.android.com/studio/index.html)
-   Eclipse [12](https://www.eclipse.org/)
-   NetBeans [13](https://netbeans.org/downloads/)
-   PyCharm
    [14](https://www.jetbrains.com/pycharm/download/#section=linux)
-   Docker (in script)
    [15](https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce)
-   Synergy (in script)
-   DropBox (only if needed for work)

``` bash
drew@drew-8570w:~$ snap list
Name                  Version                  Rev   Developer      Notes
core                  16-2.29.4.2              3604  canonical      core
drive                 current                  22    fireeye        -
juju                  2.3.1                    3106  canonical      classic
kubectl               1.9.0                    266   canonical      classic
```

Configure misc
==============

Dash to Dock
------------

<https://extensions.gnome.org/extension/307/dash-to-dock/>

Set gnome-screenshot default save directory
-------------------------------------------

?

Gnome3 Fix alt+tab to move across windows and not just grouped apps
-------------------------------------------------------------------

Application Launcher &gt; Settings &gt; Keyboard

-   Under Navgiation, Set Switch Windows to alt+tab and replace. Yes to
    confirm override of “Switch Applications”

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

Maybe Snaps
-----------

``` bash
drew@drew-8570w:~$ snap list
picard                1.4.2                    2     pachulo        -
spotify               1.0.70.399.g5ffabd56-26  5     spotify        -
sqlitebrowser-casept  3.9.1                    2     casept         -
vault                 v0.9.0                   236   snapcrafters   -
vscode                1.19.1-1513676564        22    flexiondotorg  classic
```
