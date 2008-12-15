---
title: Mplayer
layout: default
---

Video Acceleration / Video decoder offload to GPU
-------------------------------------------------

#### Xvmc For mpeg2/DVD only

Setup Xvmc - <http://www.mythtv.org/wiki/index.php/XvMC>

    mplayer -vo xvmc -vc ffmpeg12mc -dvd://1

#### VDPAU For h264/AVC, VC-1/WMV3, and Mpeg1/2

Setup VDPAU - <http://www.nvnews.net/vbulletin/forumdisplay.php?f=14>

    ./mplayer -vc ffmpeg12vdpau,ffh264vdpau,ffwmv3vdpau,ffvc1vdpau -vo vdpau some_file.avi

DVD Related
-----------

#### Run DVD copied to hard drive

    mplayer -dvd-device /mnt/raid5/drew/video_to_encode/futurama_beast_billion_backs/ dvd://

#### Force Different Language

    mplayer -alang en

or

    mplayer -aid 128

Different X Server
------------------

    mplayer -display :1

Audio Output
------------

    mplayer -ao alsa:device=hw=0.0

    mplayer -ao oss
