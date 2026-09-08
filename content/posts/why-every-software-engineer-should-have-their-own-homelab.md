+++
draft = false
date = 2026-09-08T20:00:00+01:00
title = "Why Every Software Engineer Should Have Their Own Homelab"
description = ""
slug = "why-every-software-engineer-should-have-their-own-homelab"
authors = ["Łukasz Siedlecki"]
tags = ["homelab", "proxmox", "talos", "kubernetes", "self-hosting"]
categories = ["Homelab"]
externalLink = ""
series = []
+++

I've been working in tech for a long time. Earlier in my career I hadn't thought about how powerful a homelab could be. I didn't know then what I know now. Especially in the AI era, it's important to have this kind of "playground". And now I'd like to tell you something about that.   

## Why bother with a homelab

Cloud consoles are great, but they hide a lot. I already work with cloud-native tech daily, but a homelab is where I get to break things without a blast radius that matters to anyone but me. And no, you don't have to have expensive, fancy servers to take advantage of the homelab approach. This is where I'll tell you exactly how I built my own homelab. And keep in mind: it wasn't a one-shot action. I spent a lot of time choosing the right (not too cheap, not too expensive) hardware, I spent a lot of time choosing what my main system should be, I spent a lot of time choosing what I'd like to self-host, and what I want to do with those services. And now I have a place not only for experiments, but also for "production-grade" systems like Home Assistant, which is used by me and my family.

## The hardware

I started with my TP-LINK Omada environment. Omada takes care of my networking in my whole house. I have a switch, a router, 3 indoor APs and 1 outdoor AP. It works pretty well.
Later I bought an Intel NUC mini computer. I had to add more RAM (now I have 64GB), and swap the disk for a bigger one (2 TB currently). This is my main server. 
The next one is a Lenovo ThinkStation P310, and I decided to use that one as a NAS server. I bought an 18 TB refurbished Seagate drive and put it there. And so far I am really happy with my choices. 
In my opinion it doesn't sound like super-expensive stuff. I'd say it's affordable. 


## Proxmox as the foundation

This was the first software decision I had to make. Which OS would I like to use? Bare-metal Debian was my first consideration. But I quickly realized that it wouldn't be enough. So I decided to go with Proxmox, which is a virtualization platform. Now I have a choice - I can either go with VMs and even install Debian or any other distro there, or just install some LXCs, which is really easy.
So I started with Proxmox on my NUC, and my NAS too. 

## Talos Linux on top

I won't cover every service I self-host in this article. Only the most important ones. And I think the most important thing in my homelab is my Talos Linux cluster. I wanted to learn K8s. But not the easiest way - the proper way.
Talos Linux is a Linux distribution built for one job only: running Kubernetes. It does not work like a normal Linux server. There is no SSH, no shell, and no way to log in and type commands. You manage everything through an API, using a CLI tool called talosctl.

The whole system is immutable. The filesystem does not change while it runs - you cannot install a package or edit a file by hand. To change anything, you write a new configuration in YAML and send it to the node. Talos applies it and, if needed, reboots into the new state.

This design has a nice side effect: the system is small, secure, and hard to break by accident, because there is almost nothing left to touch. Talos is written in Go, boots fast, and runs on bare metal, virtual machines, and every major cloud.

My cluster lives on three virtual machines on one of my two Proxmox nodes, sitting on their own VLAN, separate from the rest of my home network.

## What's running on the cluster

Before any app runs, the cluster needs a few base pieces. Everything here is shared by every app.

- **ArgoCD** - GitOps engine. It watches this repository and applies changes automatically - pushing to `main` is enough to deploy.
- **Longhorn** - Distributed block storage. Default storage class keeps only one replica, to save disk space.
- **MetalLB** - Gives real LoadBalancer IPs to services, from a small local range.
- **nginx-ingress** - One ingress controller, routing every app's hostname to the right service.
- **Sealed Secrets** - Secrets are encrypted before they go into Git, so the repository stays safe to commit.
- **Kafka** - Strimzi-managed cluster, two broker nodes, no ZooKeeper (KRaft mode). Used for events between services.
- **Keycloak** - Identity provider. Handles login and permissions for shortliner.

On top of that platform, three apps actually do something useful for me day to day.

- **linkding** - Bookmark manager. Simple, fast, no extras.
- **mealie** - Recipe manager for the household.
- **shortliner** - URL shortener - and my main learning project.

## shortliner, in detail

On the surface, shortliner just turns a long URL into a short one. Underneath, it is not one program - it is four separate services, each with its own database, deployed together as one Helm chart.

**apps/shortliner - services**

- **shortliner** `:8080` - The core service. Creates short links and redirects visitors to the real URL.
- **shortliner-analytics** `:8082` - Counts clicks and builds stats, without slowing down the redirect itself.
- **shortliner-payment** `:8083` - Handles paid plans. Runs with two replicas, since it matters more if this one goes down.
- **shortliner-frontend** `:3000` - The website people actually see. Talks to the other services on their internal addresses only.
