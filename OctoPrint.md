---
title: OctoPrint
layout: default
---

Using a Raspberry Pi3 running Rasbian 8

Setup OctoPrint
===============

Add your user to the dialout group;

    $ usermod -a -G dialout drew

Build
-----

    $ git clone https://github.com/foosel/OctoPrint.git
    $ cd OctoPrint
    $ virtualenv venv
    $ ./venv/bin/python setup.py install

Run
---

    $ cd ~/OctoPrint
    $ venv/local/bin/octoprint 

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

Tune Extruder and Heatbed PID
-----------------------------

Issue

    Recv: Error:Thermal Runaway, system stopped! Heater_ID:
    Changing monitoring state from 'Printing' to 'Error: Thermal Runaway, system stopped! Heater_ID: 
    '
    Recv: 9
    Changing monitoring state from 'Error: Thermal Runaway, system stopped! Heater_ID: 
    ' to 'Closed'

Need to tune:

     
    M105 # get extruder temp
    M303 # tunes to 150C
    M303 S180 # tunes to 180C
    M303 S180 C10 # tunes to 180 for 10 times
    M303 E-1 S70 C10 # Use to tune the bed at 70C
    Recv:  Ku: 57.76 Tu: 38.50
    Recv:  Classic PID
    Recv:  Kp: 35.02
    Recv:  Ki: 1.83
    Recv:  Kd: 167.82
    Recv:  Classic PID
    Recv:  Kp: 34.02
    Recv:  Ki: 1.70
    Recv:  Kd: 169.89

    # Set PIDs for Extruder
    M301 P12.33 I0.51 D74.50 # default  from Configuration.h
    M301 P33.58 I1.75 D160.93 # tuned   for extruder

    # Set PID for Heatbed
    M304 P234.88 I42.79 D322.28 # default from Configuration.h
    M304 P519.74 I72.10 D936.70 #tuned for heated bed
    Enter the following command to save the PID settings to EEPROM. 

     M500

-   <https://www.lulzbot.com/fine-tune-your-marlin-pid-settings>

Setup mjpg-streamer
===================

Add your user to the video group;

    $ usermod -a -G video drew

Build
-----

    $ git clone https://github.com/jacksonliam/mjpg-streamer.git
    $ cd mjpg-streamer-experimental
    $ make

Run
---

    $ cd ~/mjpg-streamer/mjpg-streamer-experimental/
    $  ./mjpg_streamer -i "./input_uvc.so -r 1280x720" -o "./output_http.so"
    $ uvcdynctrl -s "Focus, Auto" 1

-   Reference
    -   <http://www.sphaero.org/blog:2012:0727_control_your_webcam_from_the_command_line>

Browse
------

-   <http://192.168.1.121:8080/?action=stream>
-   <http://127.0.0.1:8080/?action=snapshot>

