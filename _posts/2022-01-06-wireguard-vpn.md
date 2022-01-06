---
layout: post
title: "WireGuard, VPN made easy"
date: 2022-01-06 10:00:00
categories: homelab self-hosted
tags: wireguard homelab self-hosted docker vpn
---

Rather than expose some services in your homelab to the _wild_ public internet, wouldn't it be better if you can access them safely anywhere you are? Maybe from your phone?
Well, I like the idea, and I set up a **VPN** to accomplish this mission.\
If you don't know what a VPN is, take a look at [this](https://en.wikipedia.org/wiki/Virtual_private_network).\
I am not going to lie, networking is not my strongest point, but [WireGuard](https://www.wireguard.com/) is so easy to set up that anyone can do it!\
I am going to use a Docker image from [linuxserver.io](https://docs.linuxserver.io/images/docker-wireguard), an amazing place to find Docker images.\
Let's move to the terminal.
```bash
mkdir wireguard
cd wireguard
touch docker-compose.yml
nano docker-compose.yml
```
`docker-compose.yml`
```yaml
---
version: "2.1"
services:
  wireguard:
    image: lscr.io/linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - SERVERURL=wireguard.domain.com #optional
      - SERVERPORT=51820 #optional
      - PEERS=1 #optional
      - PEERDNS=auto #optional
      - INTERNAL_SUBNET=10.13.13.0 #optional
      - ALLOWEDIPS=0.0.0.0/0 #optional
    volumes:
      - /path/to/appdata/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 51820:51820/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```
All environment variables are pretty much self-explanatory, which it helps in the setup process. Edit the variables as you like
and spin this container up!\
```bash
sudo docker-compose up -d
```
Once the container is up and running, take a look at the logs.
```bash
sudo docker-compose logs
```
Here you should find a **QR code** you can use with the WireGuard app on your phone. Just scan the code and your phone is going to
get the configuration automatically.\
Now you just need to go to your router setting, forward port `51820/udp` of WireGuard and you are good to go.\
_It was easy, wasn't it?_\
Of course, there is a lot more than this. Just remember: _documentation is your friend_.
