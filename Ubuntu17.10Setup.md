---
title: Ubuntu17.10Setup
layout: default
---

Install Main Apps
=================

``` bash
git config --global user.name "Drew Holt"
git config --global user.email "drewderivative@gmail.com"

sudo sh -c 'echo "drew ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'

cd $HOME; rmdir Documents/ Music/ Public/ Templates/ Videos/; rm examples.desktop

sudo dpkg-reconfigure popularity-contest # disable

sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get -y dist-upgrade

sudo apt-get install -y etckeeper

cd /etc
sudo etckeeper init
cd $HOME

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
ansible `#automation`

# Set good vim
sudo update-alternatives --set editor /usr/bin/vim.basic

# Install Oracle Java 8
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
sudo apt-get install -y oracle-java8-installer
#sudo apt-get install -y oracle-java9-installer
#sudo update-alternatives --config java
#per user JAVA_HOME="/usr/lib/jvm/java-8-oracle"

pip install youtube-dl

cat <<EOF >> $HOME/.bashrc
export PATH="$HOME/.local/bin:$PATH"
alias xclip='xclip -selection clipboard'
alias rdesktop='rdesktop -g 1280x720 -r clipboard:CLIPBOARD -r disk:share=/home/drew'
alias get_ip='_get_ip() { VBoxManage guestproperty get "$1" "/VirtualBox/GuestInfo/Net/1/V4/IP";}; _get_ip'
EOF

# docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install -y docker-ce
sudo usermod -a -G docker drew

# keybase
curl -O https://prerelease.keybase.io/keybase_amd64.deb
# if you see an error about missing `libappindicator1`
# from the next command, you can ignore it, as the
# subsequent command corrects it
sudo dpkg -i keybase_amd64.deb
sudo apt-get install -f
run_keybase

sudo apt-get install -y ./atom-amd64.deb ./google-chrome-stable_current_amd64.deb ./insync_1.4.4.37065-artful_amd64.deb ./slack-desktop-3.1.0-amd64.deb ./vagrant_2.0.3_x86_64.deb ./virtualbox-5.2_5.2.8-121009_Ubuntu_zesty_amd64.deb
```

-   Chrome, verify Google Hangouts
-   Atom [1](https://atom.io/)

``` bash
### run after installed
apm install atom-beautify linter-flake8 linter-pep8 autocomplete-python django-templates script-runner teletype
</syntaxhighlihgt>
* VirtualBox [https://www.virtualbox.org/]
<syntaxhighlight lang=bash>
echo y | sudo VBoxManage extpack install "Oracle_VM_VirtualBox_Extension_Pack-5.2.8.vbox-extpack"
```

-   Vagrant [2](https://www.vagrantup.com/)

``` bash
### run after installed
vagrant plugin install vagrant-berkshelf
vagrant plugin install berkshelf
```

-   KeyBase [3](https://keybase.io)
-   Insynq [4](https://www.insynchq.com/downloads)
-   Slack

Next
====

-   Terraform [5](https://www.terraform.io/)
-   Gitter
-   Ramlog or equivalent for SSD
-   nvm
-   gvm for goland
-   rvm [Ubuntu RVM Instructions](https://github.com/rvm/ubuntu_rvm)
-   Studio 3T (mongodb browswer) (https://studio3t.com/download/)
-   IntelliJ [6](https://www.jetbrains.com/idea/download/)
-   Android Studio [7](https://developer.android.com/studio/index.html)
-   Eclipse [8](https://www.eclipse.org/)
-   NetBeans [9](https://netbeans.org/downloads/)
-   PyCharm
    [10](https://www.jetbrains.com/pycharm/download/#section=linux)
-   Docker (in script)
    [11](https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce)
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
