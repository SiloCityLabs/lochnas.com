---
title: "Collabora"
date: 2022-11-29
description: "A powerful online office suite"
tags: ["apps", "docs", "collabora", "office"]
---

## Details

This is a template to add this container to your nas setup full functional with matching permissions and settings that of lochnas repo.

Original container [collabora/code](https://hub.docker.com/r/collabora/code)

## How to enable

Add the domain ssl replacing domain.com with the root domain you entered in your config.yml

```
/lochnas/server.bin -domain add office.{domain.com}
```

Edit your `/lochnas/docker-templates/collabora/.env` file and enable this container with `COLLABORA_ENABLED=true`. 

## Additional Configuration

You can try it in 5 minutes with Nextcloud following these basic steps:

 - In your browser go to https://cloud.yourdomain.com and set up your Nextcloud.
 - In Nextcloud go to Apps – Office and Text, and install Nextcloud Office app.
 - In Nextcloud go to Settings -> Administration -> Office
 - Select "Use your own server" and type in `https://office.yourdomain.com`
