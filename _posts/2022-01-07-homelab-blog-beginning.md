---
layout: post
title: "Homelab: the beginning"
date: 2022-01-13 10:00:00
categories: blog stories
tags: homelab blog beginning
---

## A penguin made me do it

In January 2021 I had a talk with myself and _we_ agreed that I needed a change. As I moved to a new city, I thought it was the perfect time to do something new, and so I did. I spent a couple of months exploring
what was beyond my comfort zone and, eventually, I found myself thinking about a career change. \
There was a [penguin](https://en.wikipedia.org/wiki/Tux_(mascot)) whispering in my ear...

_T: You always liked Linux! Why don't you go and find a job where you can do some Linux-Fu?_\
_M: How? There are so many technologies out there that I never used!_\
_T: Build a homelab!_

That penguin was right. I should have given the homelab idea a go, so in April 2021 I bought an old PC that I would use for my homelab, and my adventure began.\
Since I was absolutely new to the game, I spent quite some time gathering information about building and managing a homelab.
Videos, blog posts, various documentation... I thought I had to spin up some [VMs](https://en.wikipedia.org/wiki/Virtual_machine) and start playing,
but how? There were so many options, and I started feeling overwhelmed. _**That's the moment when you have to keep going, otherwise you end up doing nothing**_.
So, eventually I bumped into what would become my first hypervisor: [ProxmoxVE](https://www.proxmox.com/en/). \
I installed Proxmox on my _new_ machine, and I started the studying process.

## The revelation

After downloading the [Ubuntu Server](https://ubuntu.com/download/server) ISO, it was time to spin up my first virtual machine in my homelab.
Fortunately Proxmox is pretty easy to use, so creating a VM is a smooth experience, but once it was done, I felt lost.\
I didn't know what to do, what to install, what to learn. I was looking for ideas on the web for days, until I found something called
[Pi-hole](https://pi-hole.net/). I thought it would be cool to start with something like this, because it can also serve my home network.
In that particular moment I realised why I was having troubles finding ideas! I was so focused on this concept of the homelab as a _learning tool_
that I forgot it doesn't have just _that_ purpose. That was a game changer.\
I could learn new things while actually implementing them in a _real life_ situation.
Since that moment, looking for new projects was so easy and fun. I couldn't wait to start something new, implementing
a new feature, or even just opening up the shell and make sure everything was running fine.

## VMs are good, but containers are better

During my journey, I spun up few VMs, and soon I ran out of resources (mainly RAM) so I was looking for a solution.
The solution was [Docker](https://www.docker.com/). I'm not going into details, so, if you don't know what containerisation is,
take a look at [this](https://www.ibm.com/uk-en/cloud/learn/containerization).
Because I wanted to learn as much as I could, I installed Docker in one of my VM and started messing around.\
I remember that at first, it was a weird experience, most likely because I was still learning the basics, but the more confident I became,
the more containers I ended up spinning. Long story short, every application running in a VM was then moved in a Docker Container.
It helped me save a lot of resources and, at the same time, it set my mindset to: _**if I can run it in a container, I will!**_

## A new beginning

After a couple of months, my homelab adventure with Proxmox, few VMs and Docker, came to its end.\
Sad? Not really, because I was hungry for improvement! I decided to rebuild my homelab on top of a different hypervisor.
Don't get me wrong, I didn't have any issue with Proxmox, I just wanted something more known in the industry: [VMware ESXi](https://www.vmware.com/uk/products/esxi-and-esx.html).
Once installed and ready to go, I created a VM to serve me with Docker, set up all the containers I needed and start another
chapter of this adventure.\
I was so excited, motivated, and, more important, I had a plan!\
_But this is another story..._
