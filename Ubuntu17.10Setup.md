---
title: Ubuntu17.10Setup
layout: default
---

Install Main Apps
=================

``` bash
#!/bin/bash
set -x
set -e

START=$(date +%s)

date

# passwordless sudo for my local box
if ! sudo grep drew /etc/sudoers; then
  sudo sh -c 'echo "drew ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'
fi

# gsettings peronalizations
if [[ ! $(gsettings get org.gnome.desktop.interface clock-format) == "'12h'" ]]; then
  # set 12 hour time
  gsettings set org.gnome.desktop.interface clock-format 12h

  # set natural scrolling, GUI under 'Settings > Mouse'
  gsettings set org.gnome.desktop.peripherals.mouse natural-scroll true
  gsettings set org.gnome.desktop.peripherals.touchpad natural-scroll false

  # switch windows, not applications. GUI under 'Settings > Keyboard'
  gsettings set org.gnome.desktop.wm.keybindings switch-applications "[]"
  gsettings set org.gnome.desktop.wm.keybindings switch-applications-backward "[]"
  gsettings set org.gnome.desktop.wm.keybindings switch-windows "['<Alt>Tab']"
  gsettings set org.gnome.desktop.wm.keybindings switch-windows-backward  "['<Alt><Shift>Tab']"

  # set gnome-terminal colors
  # gsettings list-recursively  "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile/"
  # gsettings set "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile/" login-shell true
  settings=("use-theme-colors false" "login-shell true" "foreground-color \
  'rgb(255,255,255)'" "background-transparency-percent 6" "background-color 'rgb(0,0,0)'" \
  "use-theme-transparency false" "scrollback-unlimited true" "use-transparent-background true")
  profile=$(gsettings get org.gnome.Terminal.ProfilesList default)
  profile=${profile:1:-1} # remove leading and trailing single quotes
  for i in "${settings[@]}"; do
    gsettings set "org.gnome.Terminal.Legacy.Profile:/org/gnome/terminal/legacy/profiles:/:$profile/" $i
  done

  # remove clutter
  if [ -d Documents/ ]; then
    rmdir Documents/ Music/ Public/ Templates/ Videos/
    rm examples.desktop
  fi
fi

## disable popularity-contest
#sudo dpkg-reconfigure popularity-contest # disable

# oracle 8 add java repo
if [ ! -f /etc/apt/sources.list.d/webupd8team-ubuntu-java-artful.list ]; then
  sudo add-apt-repository -y ppa:webupd8team/java
  echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
  echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
fi

# update all repos, upgrade, 3600 set to 0 when debugging
#if ! find -H /var/lib/apt/lists -maxdepth 0 -mmin -10; then
  sudo apt-get update
  sudo apt-get -y dist-upgrade
#fi

# install etckeeper and initialize it
if [ ! -d /etc/.git ]; then
  sudo apt-get install -y etckeeper

  # set github here
  git config --global user.name "Drew Holt"
  git config --global user.email "drewderivative@gmail.com"

  sudo etckeeper init
fi

# install local installers already gathered
if [ ! -d /mnt/hdd ]; then
  sudo mkdir /mnt/hdd
  sudo mount /dev/vg_hdd/lv_hdd /mnt/hdd
  cd /mnt/hdd/iso_installers/ubuntu-installers
  sudo apt-get install -y ./atom-amd64.deb ./google-chrome-stable_current_amd64.deb \
    ./insync_1.4.4.37065-artful_amd64.deb ./slack-desktop-3.1.0-amd64.deb \
    ./vagrant_2.0.3_x86_64.deb ./virtualbox-5.2_5.2.8-121009_Ubuntu_zesty_amd64.deb \
    ./skypeforlinux-64.deb ./keybase_amd64.deb ./chefdk_2.4.17-1_amd64.deb
fi

# install all the software
DEBIAN_FRONTEND=noninteractive `#no prompting` sudo apt-get install -y \
keepass2 synergy gnome-tweak-tool chrome-gnome-shell `#tools` \
vim vim-scripts vim-runtime vim-doc curl xd `#systools` \
lm-sensors p7zip-full exfat-utils exfat-fuse libimage-exiftool-perl `#systools` \
ubuntu-restricted-extras gimp audacity vlc vlc-plugin-fluidsynth ffmpeg atomicparsley `#media` \
openjdk-8-jdk icedtea-8-plugin `#java` \
openssh-server fail2ban `#daemon` \
openvpn network-manager-openconnect-gnome network-manager-openvpn-gnome `#network-client` \
rdesktop freerdp2-x11 xtightvncviewer sshpass qbittorrent wireshark `#netutil` \
nmap nikto chkrootkit wavemon namebench apache2-utils mailutils `#netutils` \
virtualenv python2.7-examples python-pip `#python` \
build-essential `#build-tools` \
shellcheck sqlitebrowser yamllint highlight gawk `#dev-tools` \
lynis pandoc apt-transport-https `#misc` \
xchat pidgin `#chatapps` \
oracle-java8-installer `#oraclejava8` \
ansible `#automation`

# Set good vim
sudo update-alternatives --set editor /usr/bin/vim.basic

# set env and aliases
if ! grep rdesktop $HOME/.bashrc; then
  cat <<EOF >> $HOME/.bashrc
  export PATH="$HOME/.local/bin:$PATH"
  alias xclip='xclip -selection clipboard'
  alias rdesktop='rdesktop -g 1280x720 -r clipboard:CLIPBOARD -r disk:share=/home/drew'
  alias get_ip='_get_ip() { VBoxManage guestproperty get "$1" "/VirtualBox/GuestInfo/Net/1/V4/IP";}; _get_ip'
EOF
fi

# install youtube-dl
if [ ! -f $HOME/.local/bin/youtube-dl ]; then
  pip install youtube-dl
fi

# install awscli
if [ ! -f $HOME/.local/bin/aws ]; then
  pip install awscli
fi

# configure lm_sensors
if ! lsmod | grep coretemp; then
  sudo sensors-detect --auto
fi

# rvm install
if [ ! -d $HOME/.rvm ]; then
  gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
  \curl -sSL https://get.rvm.io | bash -s stable --ruby
fi

# virtualbox extras pack
if ! echo $(vboxmanage list extpacks) | grep 1; then
  $location="/mnt/hdd/iso_installers/ubuntu-installers/"
  echo y | sudo VBoxManage extpack install $location/Oracle_VM_VirtualBox_Extension_Pack-5.2.8.vbox-extpack
fi

# atom plugins
if ! apm list | grep teletype; then
  apm install atom-beautify linter-flake8 linter-pep8 autocomplete-python django-templates script-runner teletype
fi

# vagrant plugins
if ! vagrant plugin list | grep berkshelf; then
  vagrant plugin install vagrant-berkshelf
  vagrant plugin install berkshelf
fi

# nvm install
if [ ! -d $HOME/.nvm ]; then
  curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
fi

date

END=$(date +%s)
DIFF=$(echo "$END - $START" | bc)
```

Local Installers and config needed
==================================

-   KeyBase [1](https://keybase.io)

``` bash
run_keybase
```

-   Insynq [2](https://www.insynchq.com/downloads)

``` bash
insync start ### do some magic here so we don't have to resync 200GB of google drive
```

-   Chrome [3](https://www.google.com/chrome/)
-   Atom [4](https://atom.io/)
-   VirtualBox [5](https://www.virtualbox.org/)
-   Vagrant [6](https://www.vagrantup.com/)
-   Slack [7](https://slack.com/downloads/linux)
-   Skype [8](https://www.skype.com/en/get-skype/skype-for-linux/)
-   Docker (in script)
    [9](https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce)
-   Orackle 8 (in script)
-   rvm (in script) *requires **/bin/bash --login** or fixed shell*
    [Ubuntu RVM Instructions](https://github.com/rvm/ubuntu_rvm)
-   awscli (in script) [10](https://aws.amazon.com/cli/)
-   nvm (in script) *requires **/bin/bash --login** or fixed shell* (in
    script) [11](https://github.com/creationix/nvm)

1.  ChefDK (in script) [12](https://downloads.chef.io/chefdk)

When needed
===========

-   Terraform [13](https://www.terraform.io/)
-   Gitter
-   Ramlog or equivalent for SSD
-   gvm for golang
-   Studio 3T (mongodb browswer) (https://studio3t.com/download/)
-   Android Studio [14](https://developer.android.com/studio/index.html)
-   Eclipse [15](https://www.eclipse.org/)
-   NetBeans [16](https://netbeans.org/downloads/)
-   DropBox (only if needed for work)
-   PyCharm
    [17](https://www.jetbrains.com/pycharm/download/#section=linux)
-   IntelliJ [18](https://www.jetbrains.com/idea/download/)

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

Configure SSH keys
------------------

Create new ones or replenish from vault.

Configure GPG keys
------------------

Replenish from vault.

Set gnome-screenshot default save directory
-------------------------------------------

?

Set default downloads directory to Desktop
------------------------------------------

command for firefoxx, chrome, qbit, skype, slack, hangouts, etc

Gnome Tweak Tool
----------------

Install extension then use Tweak tool to configure.

### Dash to Dock

-   Dash to Dock
    [19](https://extensions.gnome.org/extension/307/dash-to-dock/)
-   TopIcons-plus
    [20](https://extensions.gnome.org/extension/1031/topicons/) - for
    Insync, Slack, Skype icons
-   OpenWeather
    [21](https://extensions.gnome.org/extension/750/openweather/)
-   Grown-up notifications
    [22](https://extensions.gnome.org/extension/1335/grown-up-notifications/)

Extensions installed into:

``` bash
$ ~/.local/share/gnome-shell/extensions
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
