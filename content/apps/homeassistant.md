---
title: "Home Assistant"
date: 2022-11-29
description: "On-Premises home automation platform"
tags: ["apps", "docs", "hass", "home assistant"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo.

Original maintainer [homeassistant/home-assistant](https://hub.docker.com/r/homeassistant/home-assistant)

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add hass.{domain.com}
```

Edit your `/lochnas/docker-templates/homeassistant/.env` file and enable this container with `HOMEASSISTANT_ENABLED=true`. Run `service lochnas restart` and navigate in a browser to configure nextcloud at `hass.domain.com`. This should be pretty straight forward.

## Adding dongle to container

To add a zigbee/zwave dongle to the container, you need to add the device path to your `.env` file:

Example:
```
GLOBAL_DEVICE_0=/dev/ttyUSB0
GLOBAL_DEVICE_1=/dev/ttyUSB1
GLOBAL_DEVICE_2=/dev/null
GLOBAL_DEVICE_3=/dev/null
```