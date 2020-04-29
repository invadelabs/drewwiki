---
title: MacOS
layout: default
---

macOS Mojave 10.14.4 (at the time of this writing)

First manually:

-   brew
-   synergy
-   google chrome
-   google drive
-   firefox
-   audacity
-   keybase

Then Via Brew:

``` bash
brew install ansible atomicparsley bash-completion ffmpeg git gnu-sed gnupg hub imagemagick kpcli nmap nvm openconnect openssl openvpn p7zip pstree psutils rename rbenv shellcheck telnet watch unrar wget xz
```

Add to ~/.profile

``` bash
[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"
```

Then Via Brew Cask:

``` bash
brew cask install android-file-transfer atom gimp java keepassxc osxfuse qbittorrent slack vlc tunnelblick vnc-viewer wireshark
```

After osxfuse is installed

``` bash
brew install sshfs
```

Install packages via apm (atom package manager):

``` bash
Pull from github.com/drew-holt/ubuntu_setup_bash.sh
```

Then Larger Via Brew Cask:

``` bash
brew cask install libreoffice
```

Pipe to clipboard from terminal

``` bash
cat list_of_stuff | pbcopy
```

Setup git

    populate or import ~/.gnupg/
    gpg --list-keys
    brew install pinentry-mac
    git config --global gpg.program /usr/local/bin/gpg

Other OS X Software
===================

-   XQuartz
-   Inkscape
-   SoundFlower - <https://github.com/mattingalls/Soundflower>
-   32 Lives (32-bit to 64-bit Audio Units and VST plug-ins adapter)
-   3T MongoChef
-   Android Studio
-   Arduino
-   Blender
-   Cura
-   IntelliJ IDEA CE
-   OminGraffle
-   Slic3r
-   VirtualBox
-   Xcode
-   ChefDK
-   SketchUp
-   Gitter

other brew
----------

``` bash
gradle24
maven
rvm ** using rbenv now
```

To-do
=====

-   Time Machine Backup
-   Proper Windows -&gt; Mac modifier keys
-   Make Windows key not invoke unity when in synergy or Virtualbox

