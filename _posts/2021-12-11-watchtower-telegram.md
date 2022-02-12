---
layout: post
title: "Watchtower and Telegram notifications"
date: 2021-12-11 10:00:00
categories: automation self-hosted
tags: watchtower homelab self-hosted docker alerting
---

Updates... It could be a tedious task, but it has to be done.\
If you run containers in your homelab, you can easily get to the point where manually update all of your container images
becomes a boring moment of your day. It would be nice if we can delegate this task to someone else and, maybe, receive a notification
once all it's done. Well, fortunately we can do this with [Watchtower](https://github.com/containrrr/watchtower)!

**IMPORTANT!** _Despite we can automate this boring task, my advice is to not do it and always update manually.\
Check the release notes first! Update always with the newest release might not be worth_.

To give it a go, we firstly need to create a **Telegram Bot** for Watchtower. We can ask the [BotFather](https://telegram.me/BotFather)
to guide us in the process. When the bot creation is done, BotFather will give us our **_BOT_TOKEN_**. Keep it safe, we will need it later!\
Once we have our token, we need to get our **_CHAT_ID_** with [GetIDsBot](https://telegram.me/getidsbot).\
_It's so exciting to create our personal bot, isn't it?_\
So, now it's time to get our hands dirty into the terminal.
I chose the docker-compose way. So...

```bash
mkdir watchtower
cd watchtower
touch docker-compose.yml
nano docker-compose.yml
```
`docker-compose.yml`

```yaml
---
version: '3.3'

services:
  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    restart: unless-stopped
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
    environment:
      - TZ=Europe/London
      - WATCHTOWER_LIFECYCLE_HOOKS=True
      - WATCHTOWER_NOTIFICATIONS=shoutrrr
      - WATCHTOWER_NOTIFICATION_URL=telegram://BOT_TOKEN@telegram/?channels=CHAT_ID
      - WATCHTOWER_DEBUG=true
      - WATCHTOWER_CLEANUP=true
      - WATCHTOWER_SCHEDULE=0 0 20 * * 0
```
Watchtower uses _shoutrrr_ to send notifications via different applications.\
Just replace _BOT_TOKEN_ and _CHAT_ID_ with your own ones, and it's done!\
With this setup, Watchtower will do its _magic_ every sunday at 20:00 (8:00pm), sends us notifications through our Telegram Bot
and delete the old images. Once we set all up, we can write and save the file.\
Now we can create our Watchtower container with:
```bash
sudo docker-compose up -d
```
If everything goes well, we should receive a Telegram notification from our Watchtower Bot telling us when the first check
will be performed.

You can always refer to the [Watchtower Documentation](https://containrrr.dev/watchtower/) if you want to play around.
