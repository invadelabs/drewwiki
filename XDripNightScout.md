---
title: XDripNightScout
layout: default
---

NightScout
----------

### Install NVM

NightScout install NVM

``` bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
$ nvm install 0.10.42
$ nvm use 0.10.42
```

### Clone and Build

``` bash
$ git clone https://github.com/nightscout/cgm-remote-monitor.git
$ cd cgm-remote-monitor
$ npm install
```

### Setup my.env

``` bash
$ cat my.env 
MONGO_CONNECTION=mongodb://user:password@my_mongodb_host:27071
MONGO_COLLECTION=entries
DISPLAY_UNITS=mg/dl
API_SECRET=my_api_secret
CUSTOM_TITLE=Drew
THEME=colors

#TREATMENTS_AUTH=on

ALARM_URGENT_HIGH=off
ALARM_HIGH=off
ALARM_LOW=off
ALARM_URGENT_LOW=off

DEVICESTATUS_ADVANCED="true"
```

### Start NightScout

``` bash
env $(cat my.env) ENABLE="pump careportal iob cob basal" PUMP_FIELDS="reservoir battery" node server.js
```

### NightScout API

``` bash
https://drew.invadelabs.com/api/v1/entries
https://drew.invadelabs.com/api/v1/current 

https://apisecretkey@drew.invadelabs.com/api/v1/entries
```

mmcsv MiniMed Connect to CSV / JSON
-----------------------------------

``` bash
$ git clone https://github.com/LittleDMatt/mmcsv.git
$ vi lib/utils.js
 change to US time stamp
// changed date format from MM/DD/YYTHH:mm:ss
var CARELINK_TIME = 'MM/DD/YYTHH:mm:ss';
var OUTPUT_TIME_MASK = 'YYYY-MM-DDTHH:mm:ss';

$ bin/mmcsv fetch --username $CARELINK_USERNAME --password $CARELINK_PASSWORD$ --days 30 > ~/this.csv

$ bin/mmcsv parse ~/this.csv > ~/bla.json

Upload to nightscout:
$ curl -vs -X POST --header "Content-Type: application/json" --header "Accept: application/json" --header "api-secret:my_api_secret" --data-binary @bla.json "http://192.168.1.124:1337/api/v1/treatments"
```

xDrip
-----

xDripPebble
-----------
