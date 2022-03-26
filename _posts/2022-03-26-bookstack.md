---
layout: post
title: "Documentation, Documentation, Documentation!"
date: 2022-03-18 10:00:00
categories: homelab self-hosted
tags: bookstack homelab self-hosted docker documentation
---

Recently someone asked on Reddit: _"What's your number one recommended service?"_\
Everyone could answer this question differently, but my answer was: _"Bookstack. Start documentation as soon as possible!"_.
This is a piece of advice I would give to myself at the very beginning. Of course, working on projects like setting up a media
server could be fun, and also you can _use_ it almost immediately. Documentation is something that most of us (me included!) tend
to postpone with a plethora of _excuses_. I thought documentation is useful only when working on _big_ projects, not for a
homelab, but you can always find something to write in the documentation. You can write your configurations, detailing the steps
to set up your homelab, issues you encountered and how you fixed or dealt with them... the list goes on and on.\
Nobody taught me how to write documentation, and I am sure it's not great, but I am doing my best, and I am keeping track of
what I am doing in my homelab.\
So, as you probably guessed, I use [Bookstack](https://www.bookstackapp.com/) for my documentation. Some people may prefer
a _Wiki-style_ application, but I like the idea of having **Books**, **Chapters** and **Pages**, and it's very easy to use.\
I don't think I need to say that I used docker-compose to set it up, but if you fancy something different you can read the
[documentation](https://www.bookstackapp.com/docs/admin/installation/).
```bash
mkdir bookstack
cd bookstack
touch docker-compose.yml
nano docker-compose.yml
```
`docker-compose.yml`
```yaml
---
version: "2"
services:
  bookstack:
    image: lscr.io/linuxserver/bookstack
    container_name: bookstack
    environment:
      - PUID=1000
      - PGID=1000
      - APP_URL=
      - DB_HOST=bookstack_db
      - DB_USER=bookstack
      - DB_PASS=<yourdbpass>
      - DB_DATABASE=bookstackapp
    volumes:
      - /path/to/data:/config
    ports:
      - 6875:80
    restart: unless-stopped
    depends_on:
      - bookstack_db
  bookstack_db:
    image: lscr.io/linuxserver/mariadb
    container_name: bookstack_db
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=<yourdbpass>
      - TZ=Europe/London
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=<yourdbpass>
    volumes:
      - /path/to/data:/config
    restart: unless-stopped
```
Setting up the environment variables is pretty straightforward, just pay attention to match the database passwords.
```bash
sudo docker-compose up -d
```
Now, if you didn't read the documentation (naughty!), you can login using `admin@admin.com` and password of `password`.

**_Go and write your own documentation!_**
