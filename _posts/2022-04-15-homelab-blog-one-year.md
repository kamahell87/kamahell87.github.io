---
layout: post
title: "A year later"
date: 2022-04-15 17:00:00
categories: blog stories
tags: homelab blog anniversary
---

Time flies when you are having fun! \
I spent the last year learning, tinkering, testing, getting mad... but I'm still here, ready to do it again and again! \
Doing all these things while in a full time job is not easy. Sometimes when you come back from work you just want to rest
and chill, and it's difficult to find the strength to carry on. So, it was challenging, but also fun and rewarding. \
Let's wrap it up!

### New setup

I changed the setup after a couple of months, and this is what I have done:

* Bought a _new_ machine and migrated all my Docker containers there
* Get rid of Proxmox and installed ESXi instead
  * Set up few VMs for testing and practice with **Ansible**
* Bought a _HP Proliant Microserver N40L_ and installed **OpenMediaVault** on it

Now I have a bigger playground, and I feel more in control (mainly because I know I have backups on my NAS). \
Recently I destroyed all the VMs in ESXi and set up a 5 nodes **Kubernetes** cluster using **K3s**.

### The biggest win

Maybe for some people this is not considered a _big win_, but it is for me. \
I coded a simple Telegram Bot in **Python** and created a container image of it. I then created a deployment for this bot
in my **K3s** cluster. For the final touch, I set up **ArgoCD** to monitor the repository where the deployment manifest is,
so if I want to change something (e.g. put the bot in _maintenance mode_) I can just edit the manifest and ArgoCD will do
the rest for me.

### The biggest fail

I guess this is a common mistake... \
One of the first thing I have tried with Ansible was trying to configure _sshd_config_. The idea was simple, just change
SSH port, disable root login, and set up _AllowUsers_. \
_I know you already guessed where this is going..._ \
So, I set the template out, set the _AllowUsers_ with a user I had on a **different** machine and run the playbook.
Everything went fine without any errors, but I soon realised I messed up the user and locked myself out of that machine.
Luckily I had physical access to that machine, so I managed to get in and fix my mistake. This is something that will not
happen again.

### A piece of advice

I really enjoy administering my home lab, trying to improve things, implement automation when I can... it's so much fun!
As I said earlier, sometimes could be challenging if you are in a full time job. You are constantly thinking how to fix
that issue, or how to automate _this_ or _that_, what technology you need to learn, and so on... \
If you are in the same situation and you are struggling to keep it up, keep this in mind: **it's ok to take a break**.
