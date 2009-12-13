---
title: EGalaxyTouchScreen
layout: default
---

Intsall evtouch;

    # sudo apt-get install xserver-xorg-input-evtouch

Modify /etc/X11/xorg.conf;

    Add to Section "ServerLayout"
            InputDevice "touchscreen" "CorePointer"

    Add new section;
    Section "InputDevice"
        Identifier "touchscreen"
        Driver "evtouch"
        Option "Device" "/dev/input/event10"
        Option "DeviceName" "touchscreen"
        Option "MinX" "98"
        Option "MinY" "43"
        Option "MaxX" "940"
        Option "MaxY" "925"
    #    Option "ReportingMode" "Raw"
    #    Option "Emulate3Buttons"
    #   Option "Emulate3Timeout" "50"
        Option "SendCoreEvents" "On"
        Option "SwapY" "true
    EndSection

Had to;

    # rmmod usbhid
    # insmod usbtouchscreen

Restart X;

    # sudo restart gdm

Unable to get ev\_calibrate to work

How to use egalax driver; DL latest driver from eeti.com

    tar zxvf 
    cd USBSrc
    vi tkusb.h

change asm/semaphore.h to linux/semphore.h

    make
    cp tkusb.ko /lib/modules 
    vi /etc/rc.local
    rmmod usbhid
    insmod /lib/modules/tkusb.ko
    vi /usr/share/hal/fdi/policy/20thirdparty/50-eGalaxy.fdi
    evtouch -> egalax
    Xorg -configure
    cp -i ~/xorg.conf.new /etc/X11/xorg.conf
    sudo sh setup.sh
    sudo restart gdm
