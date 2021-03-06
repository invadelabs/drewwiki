---
title: LircPinnacle800iComcastRemote
layout: default
---

/var/log/messages shows errors like the following for the unmapped
buttons on the remote.

``` bash
messages.0:Dec 10 15:08:35 drew-desktop kernel: [81408.914101] cx88 IR (Pinnacle PCTV HD 800i): unknown key: key=0x3b raw=0x317b down=0
```

Use key=**0x3b** or whatever key reported to modify ir-keymap.c

Module Compile
--------------

``` bash
sudo apt-get build-dep linux-source-2.6.24
sudo apt-get install linux-source-2.6.24 build-essential
tar -jxvf /usr/src/linux-source-2.6.24.tar.bz2
ln -sf linux-source-2.6.24 linux
cd linux/drivers/media/common
vi ir-keymap.c
make -C /lib/modules/`uname -r`/build/ M=`pwd` modules
strip --strip-debug ir-common.ko
sudo install -m644 -b ir-common.ko /lib/modules/`uname -r`/kernel/drivers/media/common
sudo depmod -ae
sudo update-initramfs -u
sudo reboot
```

Changes to ir-keymap.c
----------------------

``` c
/* Pinnacle PCTV HD 800i mini remote */
IR_KEYTAB_TYPE ir_codes_pinnacle_pctv_hd[IR_KEYTAB_SIZE] = {

        [0x01] = KEY_1,
        [0x02] = KEY_2,
        [0x03] = KEY_3,
        [0x04] = KEY_4,
        [0x05] = KEY_5,
        [0x06] = KEY_6,
        [0x07] = KEY_7,
        [0x08] = KEY_8,
        [0x09] = KEY_9,
        [0x00] = KEY_0,

/* XXnot on this remote [0x24] = KEY_ZOOM,
        [0x2a] = KEY_SUBTITLE, */

/* XXnot on this remote [0x00] = KEY_MUTE, */
        [0x0b] = KEY_ENTER,     /* Pinnacle Logo */
        [0x0c] = KEY_POWER,

/* XXnot on this remote [0x03] = KEY_VOLUMEUP,
        [0x09] = KEY_VOLUMEDOWN, */
        [0x20] = KEY_CHANNELUP,
        [0x21] = KEY_CHANNELDOWN,

        [0x32] = KEY_REWIND,
        [0x35] = KEY_PLAYPAUSE,
        [0x34] = KEY_FASTFORWARD,
        [0x36] = KEY_STOP,
        [0x37] = KEY_RECORD,
        [0x3e] = KEY_EPG,       /* Labeled "?" */
        [0x29] = KEY_PAUSE,     /* Labeled "?" */
        [0x3b] = KEY_LAST,      /* Labeled "?" */
};
EXPORT_SYMBOL_GPL(ir_codes_pinnacle_pctv_hd);
```

Comcast remote
--------------

AUX - I think it was code 1081 or 0180
