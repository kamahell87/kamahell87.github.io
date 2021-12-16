---
layout: post
title: "Lychee, not the fruit"
date: 2021-12-16 10:00:00
categories: homelab self-hosted
tags: lychee homelab self-hosted docker photo-management-system
---

Do you like lychees? I bet you will like this one!\
Few weeks ago, I was looking for a self-hosted solution where I can store all my travel pictures and I eventually bumped into [Lychee](https://github.com/LycheeOrg/Lychee).
Lychee is a free, simple and secure photo-management-system which can be run in a Docker container. Which is basically what
I was looking for! So I decided to try it out and... I loved it!\
That's how I have done it. First, I needed a _big room_ for my pictures. A shared folder in my NAS would do the job.\
I needed two more folders: a **database** folder (yes, we need a database) and a **config** folder.\
Once created these folders, it was time to create the containers.

```bash
mkdir lychee
cd lychee
touch docker-compose
nano docker-compose
```
`docker-compose.yml`
```yaml
version: '3'

services:
  lychee_db:
    container_name: lychee_db
    image: mariadb:10
    environment:
      - MYSQL_ROOT_PASSWORD=YourSuperSecretRootPassword
      - MYSQL_DATABASE=lychee
      - MYSQL_USER=YourUsername
      - MYSQL_PASSWORD=YourSuperSecretPassword
    expose:
      - 3306
    volumes:
      - /path/to/db:/db

    networks:
      - lychee
    restart: unless-stopped

  lychee:
    image: lycheeorg/lychee
    container_name: lychee
    ports:
      - 90:80
    volumes:
      - /path/to/config:/conf
      - /path/to/uploads:/uploads
    networks:
      - lychee
    environment:
       - PUID=1000
       - PGID=1000
       - PHP_TZ=Europe/London
       - DB_CONNECTION=mysql
       - DB_HOST=lychee_db
       - DB_PORT=3306
       - DB_DATABASE=lychee
       - DB_USERNAME=YourUsername
       - DB_PASSWORD=YourSuperSecretPassword # has to match the above MYSQL_PASSWORD
       - STARTUP_DELAY=30
    restart: unless-stopped
    depends_on:
      - lychee_db

networks:
  lychee:

volumes:
  mysql:
```
After adding all variables and volumes, just write, save the changes and then:
```bash
sudo docker-compose up -d
```
Once the containers were up and running, I opened up a web browser and headed to the `ip address:port` where Lychee lives, set up username
and password, and _ta-dah_! I now have my self-hosted photo-management-system.\
I can _upload_, _download_, _share_, get details of my pictures, implement _2FA_... It's simply amazing!\
I hope you like it too.

If you would like to personalise this service even more, take a look at the [Lychee Documentation](https://lycheeorg.github.io/docs/)
and edit the `docker-compose.yml` accordingly.
