---
title: ForceTextConsoleResolution
layout: default
---

/etc/default/grub

    GRUB_TIMEOUT=5
    GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
    GRUB_DEFAULT=saved
    GRUB_DISABLE_SUBMENU=true
    GRUB_TERMINAL_OUTPUT="console"
    GRUB_CMDLINE_LINUX="rd.lvm.lv=fedora_drew-serv/root rd.lvm.lv=fedora_drew-serv/swap nomodeset" # <---- nomodeset!!!!
    GRUB_DISABLE_RECOVERY="true"
    GRUB_GFXPAYLOAD="1024x768x32"
    GRUB_GFXPAYLOAD_LINUX="1024x768x32"
    GRUB_VIDEO_BACKEND="vbe"
    GRUB_TERMINAL_OUTPUT="gfxterm"
    GRUB_FONT_PATH="/boot/grub2/fonts/unicode.pf2"
    GRUB_GFXMODE="1024x768x32"
