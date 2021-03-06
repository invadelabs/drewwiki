---
title: Ubuntu17.10Setup
layout: default
---

Install Main Apps
=================

Run install script from
[1](https://github.com/drew-holt/ubuntu-setup-bash/blob/master/drew-8570w_u1710setup.sh)

``` bash
wget https://raw.githubusercontent.com/drew-holt/ubuntu-setup-bash/master/drew-8570w_setup.sh
chmod 755 drew-8570w_setup.sh
./drew-8570w_setup.sh | tee -a setup-$(date '+%Y-%m-%d-%H.%M.%S%z').log
```

Installers needing extra config
===============================

-   KeyBase [2](https://keybase.io)

``` bash
run_keybase
```

-   Insync [3](https://www.insynchq.com/downloads)

``` bash
insync start ### do some magic here so we don't have to resync 200GB of google drive
```

-   Chrome [4](https://www.google.com/chrome/)
-   Atom [5](https://atom.io/)
-   Slack [6](https://slack.com/downloads/linux)
-   Skype [7](https://www.skype.com/en/get-skype/skype-for-linux/)
-   Oracle JDK 8
    [8](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-ubuntu-16-04)
-   Docker
    [9](https://docs.docker.com/install/linux/docker-ce/ubuntu/#upgrade-docker-ce)
-   awscli [10](https://aws.amazon.com/cli/)
-   youtube-dl (pip) [11](https://rg3.github.io/youtube-dl/)
-   nvm *requires **/bin/bash --login** or fixed shell*
    [12](https://github.com/creationix/nvm)
-   rvm *requires **/bin/bash --login** or fixed shell* [Ubuntu RVM
    Instructions](https://github.com/rvm/ubuntu_rvm)

Install Manually
----------------

-   VirtualBox (script this?) [13](https://www.virtualbox.org/)
-   Vagrant (script this?) [14](https://www.vagrantup.com/)
-   ChefDK (script this) [15](https://downloads.chef.io/chefdk)

When needed
===========

-   Terraform [16](https://www.terraform.io/)
-   Gitter
-   Ramlog or equivalent for SSD
-   gvm for golang
-   Studio 3T MongoDB Browser [17](https://studio3t.com/download/)
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

command for firefox, chrome, qbit, skype, slack, hangouts, etc

Gnome Tweak Tool
----------------

Install and configure extensions (done via script).

-   Dash to Dock
    [23](https://extensions.gnome.org/extension/307/dash-to-dock/)
-   TopIcons-plus
    [24](https://extensions.gnome.org/extension/1031/topicons/) - for
    Insync, Slack, Skype icons

Gmail to handle mailto: links
-----------------------------

Partially scripted.

<https://developers.google.com/web/updates/2012/02/Getting-Gmail-to-handle-all-mailto-links-with-registerProtocolHandler>

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
