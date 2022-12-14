---
title: "LochNAS Folder Structure"
date: 2022-11-29
description: "Folder structure of LochNAS server."
tags: ["folders", "paths"]
---

See folder tree in table of contents

## **/lochnas/**

Path to the root of the lochnas folder. This should live in the root folder of the server. We no longer support dynamic paths so that the containers can refference the same root paths internally and reduce user confusion.

Files:
 - `config.yml` - This contains server configuration.
 - `server.bin` - Lochnas server binary for Linux


### **home/**

User data storage path. Also excluded from git. This directory is where apps like nextcloud and plex access stored data. You can mount additional disks and [raid](./raid.md) partitions to this folder. Example: `/lochnas/home/4TB_HDD/`


### **docker-data/**

This is where apps store any persistent data. The subdirectory is the app name. This folder is excluded from git.


### **docker-templates/**

This is where apps store their templates. The subdirectory is the app name. This folder is excluded from git. Files belonging to an app:


```
    docker-templates/
    ├── app_name/
    │   ├── docker-compose.yml (required)
    │   ├── nginx.conf (optional)
    │   ├── .env.example (required)
    │   ├── after-start.sh (optional)
    │   ├── before-start.sh (optional)
    │   └── readme.md (required)
```

#### **docker-compose.yml**

Required. This is the docker-compose.yml file for the app. The app should mount volumes based on the file structure and store persistent data in the `docker-data` folder. You can look at this [simple version](../docker-templates/phpmyadmin/docker-compose.yml) or a more [complicated custom image](../docker-templates/samba/docker-compose.yml) of the docker-compose.yml file.

#### **nginx.conf**

Optional. This is the nginx configuration file for the app. When using this you must use the ${GLOBAL_DOMAIN} variable in the nginx.conf file along with a subdomain for the app. A basic example of one would be the [homeassistant nginx config file](../docker-templates/homeassistant/nginx.conf). Although every app has its own way it needs to be proxied.

#### **.env.example**

Required. This is the .env file for the app. It should be called from the docker-compose.yml file. It must have a boolean variable called `APPNAME_ENABLED` that is set to `false` by default. Only add required variables for the app to work and provide a link to documentation for more variables. Required static variables such as port and hostname configs should be set in the docker-compose.yml file instead. Variables that start with "GLOBAL_" are loaded into host os for use in docker-compose.yml (Eg: Homeassistant).

#### **after-start.sh**

Optional. This is a bash script that is run after the app is started. This is useful for settings up non persistent commands to run withouth modifying the original container. Such as a maintenance script.

#### **before-start.sh**

Optional. This is a bash script that is run before the app is started but after any port/domain checks. This is useful for settings up non persistent commands to run withouth modifying the original container. Such as a maintenance script.

#### **readme.md**

Requred. This is a markdown file that links to the lochnas.com app page.

### **server/**

The source folder for the lochnas server daemon.
