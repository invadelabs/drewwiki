---
title: Ubuntu17.10Setup
layout: default
---

Install Main Apps
=================

Run install script from
[1](https://github.com/drew-holt/u1710-setup-bash/blob/master/drew-8570w_u1710setup.sh)

``` bash
wget https://raw.githubusercontent.com/drew-holt/u1710-setup-bash/master/drew-8570w_u1710setup.sh
chmod 755 drew-8570w_u1710setup.sh
./drew-8570w_u1710setup.sh | tee -a setup-$(date '+%Y-%m-%d-%H.%M.%S%z').log
```

Additional install script for extra
[2](https://github.com/drew-holt/u1710-setup-bash/blob/master/drew-8570w_u1710setup_extra.sh)

``` bash
wget https://raw.githubusercontent.com/drew-holt/u1710-setup-bash/master/drew-8570w_u1710setup_extra.sh
chmod 755 drew-8570w_u1710setup_extra.sh
./drew-8570w_u1710setup_extra.sh | tee -a setup-$(date '+%Y-%m-%d-%H.%M.%S%z').log
```

Installers needing extra config
===============================

-   KeyBase [3](https://keybase.io)

``` bash
run_keybase
```

-   Insync [4](https://www.insynchq.com/downloads)

``` bash
insync start ### do some magic here so we don't have to resync 200GB of google drive
```

-   Chrome [5](https://www.google.com/chrome/)
-   Atom [6](https://atom.io/)
-   Slack [7](https://slack.com/downloads/linux)
-   Skype [8](https://www.skype.com/en/get-skype/skype-for-linux/)
-   Oracle JDK 8
    [9](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04)
-   awscli (pip) [10](https://aws.amazon.com/cli/)
-   youtube-dl (pip) [11](https://rg3.github.io/youtube-dl/)
-   rvm *requires **/bin/bash --login** or fixed shell* [Ubuntu RVM
    Instructions](https://github.com/rvm/ubuntu_rvm)
-   nvm *requires **/bin/bash --login** or fixed shell*
    [12](https://github.com/creationix/nvm)

Without repos:

-   VirtualBox (script this?) [13](https://www.virtualbox.org/)
-   Vagrant (script this?) [14](https://www.vagrantup.com/)
-   Docker (script this?)
    [15](https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce)
-   ChefDK (script this) [16](https://downloads.chef.io/chefdk)

When needed
===========

-   Terraform [17](https://www.terraform.io/)
-   Gitter
-   Ramlog or equivalent for SSD
-   gvm for golang
-   Studio 3T (mongodb browswer) (https://studio3t.com/download/)
-   Android Studio [18](https://developer.android.com/studio/index.html)
-   Eclipse [19](https://www.eclipse.org/)
-   NetBeans [20](https://netbeans.org/downloads/)
-   DropBox (only if needed for work)
-   PyCharm
    [21](https://www.jetbrains.com/pycharm/download/#section=linux)
-   IntelliJ [22](https://www.jetbrains.com/idea/download/)

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

Pull from vault, set git config

``` bash
gpg --import drewholt-private-2018.03.01.key
gpg --edit-key {KEY} trust quit

git config --global user.signingkey 7A27C99359698874

vi ~/.gnupg/gpg.conf:
default-key 2018-03-01

gpg -d somefile.tar.xz.pgp | tar -tJ
```

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
    [23](https://extensions.gnome.org/extension/307/dash-to-dock/)
-   TopIcons-plus
    [24](https://extensions.gnome.org/extension/1031/topicons/) - for
    Insync, Slack, Skype icons
-   OpenWeather
    [25](https://extensions.gnome.org/extension/750/openweather/)
-   Grown-up notifications
    [26](https://extensions.gnome.org/extension/1335/grown-up-notifications/)

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
