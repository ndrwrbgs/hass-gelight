# hass-gelight

## LICENSE
⚠️ Please note that this fork includes modifications which are released under GNU GPLv3. https://choosealicense.com/licenses/gpl-3.0/

### _Why GNU GPLv3?_

GNU GPLv3 is a [copyleft license](https://fossa.com/blog/all-about-copyleft-licenses/) - meaning it has a strong open-source philosophy and restricts what entities attempting to use the software for profit may do with it. 

If you are working in FOSS or nonprofit spaces, and some situation requires that you use need the code under another license, please contact me to discuss the details.

## What is it
This Home assistant custome components works for C by GE Smart Lights.
E.g.
https://www.gelighting.com/smart-home/led-bulbs

Tested it on Soft white and tunable white bulbs. It may work on Full color.
GE lights are inexpensive because the Smart light is not Smart enough...
You are supposed to locally connect to the GE Mesh through Bluetooth.
Only one device can connect. So you have to choose to between the GE app or Google home to control them.

This code use the Home Assistant as the Hub to control GE lights so all your smart devices could be used to connect to the light via the Hub.

## Requirement:
* Install bluepy and dimond. 

Note this might be done automatically by home assistant. The libraries are installed to ~/.homeassistant/deps/lib/python3.9/site-packages/.
Bluepy had a bug in described in https://github.com/IanHarvey/bluepy/issues/239 on aarch64.
Please mannually fix it by applying the patch https://github.com/IanHarvey/bluepy/files/3800265/0001-Bugfix-of-high-CPU-usage.patch.txt
to the file bluepy-helper.c and run make under the directory bluepy.
Othewise, you might notice bluepy-helper use 100% CPU resources.

* Register a C by GE account and add your devices to C by GE app.
* Extract device info using steps from https://github.com/google/python-laurel.
  * Run python3 getconfig.py
  * Example output:
```yaml
light:
  - platform: gelight
    password: %s
    username: %s
    lights:
      - id: %s
        mac: %s
        name: %s
        type:  17
      - id: %s
        mac: %s
        name: %s
        type:  20
```
* paste the output to configuration.yaml.

## Optional Requirement:
* Circadian Lighting https://github.com/claytonjn/hass-circadian_lighting


## Documentation

Account API documentation can be [found
here](https://xlink.gitbooks.io/sdk-app/content/app_user_restful/yonghu_shen_fen_jie_kou.html)
(in Chinese).
