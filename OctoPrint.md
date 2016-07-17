---
title: OctoPrint
layout: default
---

Setup OctoPrint
===============

Build
-----

    $ git clone https://github.com/foosel/OctoPrint.git
    $ cd OctoPrint
    $ virtualenv venv
    $ ./venv/bin/python setup.py install

Run
---

$ cd ~/OctoPrint $ venv/local/bin/octoprint

Browse
------

-   <http://192.168.1.121:5000/>

Add plugins
-----------

-   Settings &gt; Plugin-in Manager
    -   SnapStream (0.2.3)
    -   CuraEngine
    -   DisplayProgress
    -   Cost estimator
    -   DisplayZ
    -   EEPROM Marlin Editor
    -   Navbar Temp
    -   Filament Sensor
    -   Print History
    -   Printer Statistics
    -   StatusLine

Setup mjpg-streamer
===================

Build
-----

    $ git clone https://github.com/jacksonliam/mjpg-streamer.git
    $ cd mjpg-streamer-experimental
    $ make

Run
---

    $ sudo ./mjpg_streamer -i "./input_uvc.so -r 1280x720" -o "./output_http.so"

Browse
------

-   <http://192.168.1.121:8080/?action=stream>
-   <http://127.0.0.1:8080/?action=snapshot>

