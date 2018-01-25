---
title: RaspberryPi
layout: default
---

Debian Weezy on Raspberry Pi

RPi CPU Tempurature
-------------------

``` bash
# /opt/vc/bin/vcgencmd measure_temp
# cat /sys/class/thermal/thermal_zone0/temp
49768
# expr `cat /sys/class/thermal/thermal_zone0/temp` / 1000 # divide by 1000 for C
50
```

Force Sleep Mode / Screen off
-----------------------------

``` bash
Off: /opt/vc/bin/tvservice -o
On: /opt/vc/bin/tvservice -p
```

HDMI Audio Issues
-----------------

Append to /boot/config.txt;

``` bash
hdmi_force_hotplug=1
hdmi_drive=2
```

Reduce Wear Leveling
--------------------

``` bash
$ cat /etc/fstab
proc            /proc           proc    defaults        0       0
/dev/mmcblk0p1  /boot           vfat    defaults        0       2
/dev/mmcblk0p2  /               ext4    defaults,noatime  0     1
# a swapfile is not a swap partition, so no using swapon|off from here on, use  dphys-swapfile swap[on|off]  for that
tmpfs /var/log tmpfs defaults 0 0
```

<http://www.raspberrypi.org/phpBB3/viewtopic.php?f=29&t=13889>

``` bash
sudo apt-get install lsof rsync; dpkg -i ramlog*.deb; reboot twice
```

MP3 Plackback
-------------

``` bash
sox, or rather AUDIODEV=hw:1 play
moc or mocp
mpd
```

Software to Install
-------------------

``` bash
sudo apt-get install \
tightvncserver youtube-dl synergy transmission-daemon \
chromium \
nginx php5 php-apc php5-sqlite sqlite mailutils python dns-utils \
php5-cgi php5-fpm php5-cli
```

raspi-config autologin not as user pi
-------------------------------------

By default when setting to enable straight to desktop, this script will
make it pi;

``` bash
# /usr/bin/raspi-config
update-rc.d lightdm enable 2
sed /etc/lightdm/lightdm.conf -i -e "s/^#autologin-user=.*/autologin-user=pi/"
```

RDP with rdesktop and xfreerdp
------------------------------

``` bash
$ rdesktop -g 1280x720 -u drew -r sound=local 192.168.1.10
sound is choppy, clipboard works
-f for full, ctrl+alt+enter to exit
keymap is broken, found doesn't work??
$ xfreerdp -u drew -g 1280x720 -x l --plugin rdpsnd --data alsa -- 192.168.1.10
-x experience, l is for lan
-z is compression
```

LXDE autostart synergyc
-----------------------

``` bash
# mkdir ~/.config/autostart
# cat ~/.config/autostart/synergyc.desktop
[Desktop Entry]
Type=Application
Exec=/usr/bin/synergyc 192.168.1.10
```

Fix Time / Date
---------------

``` bash
dpkg-reconfigure tzdata
```

^ set locale

Sound
-----

``` bash
# amixer get PCM
# amixer set PCM 20%
```

^ one off to set lower noise <http://man.he.net/man1/amixer>

``` bash
# alsamixer
```

^ tui to set PCM volume / sound card info

``` bash
# amixer cset numid=3 1
```

^ 1 for headphones, 0 for hdmi

Video with omxplayer
--------------------

``` bash
# omxplayer -o local <filename>
```

^ head phones output

``` bash
# omxplayer -o hdmi <filename>
```

^ hdmi output

``` bash
# omxplayer -r <filename>
```

^ full screen, skewed though?

``` bash
# setterm -blank force && omxplayer filename
# setterm -blank poke
```

^ command on console so only the video shows (and not console text
scroll back), poke gets it back

### omxplayer - Key bindings

``` bash
1 Increase Speed
2 Decrease Speed
j Previous Audio stream
k Next Audio stream
i Previous Chapter
o Next Chapter
n Previous Subtitle stream
m Next Subtitle stream
s Toggle subtitles
q Exit OMXPlayer
Space or p Pause/Resume
- Decrease Volume
+ Increase Volume
Left Seek -30
Right Seek +30
Down Seek -600
Up Seek +600
```

Admin groups
------------

be in these groups: s/:pi/:pi,drew/

``` bash
drew@drew-rpi ~ $ grep pi /etc/group
adm:x:4:pi,drew
dialout:x:20:pi,drew
cdrom:x:24:pi,drew
sudo:x:27:pi,drew,drew
audio:x:29:pi,drew
video:x:44:pi,drew
plugdev:x:46:pi,drew
games:x:60:pi,drew
users:x:100:pi,drew
pi:x:1000:
netdev:x:105:pi,drew
input:x:999:pi,drew
```
