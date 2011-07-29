---
title: BootOptimization
layout: default
---

Readahead

systemd has a built-in readahead implementation is not enabled on
upgrades. It should improve bootup speed but your mileage may vary
depending on your hardware. To enable it:

    # systemctl enable systemd-readahead-collect.service
    # systemctl enable systemd-readahead-replay.service
