---
title: Home Lab
showSummary: true
summary: Description of my Home Lab Setup
showDate: false
showReadingTime: false
showHeadingAnchors: false
---

One of my hobbies is home labbing with old hardware. I love taking something that is supposedly obsolete (and therefore inexpensive) and turning it into a usable part of my lab. It is also incredibly rewarding and freeing to know that I am running my own services on my own hardware. 

Remote access is secured via VPN. I take security very seriously and have been intentionally careful to not expose my home network.

Below is a list of my current home lab setup:

## Desktop Computer
- 2014 iMac
- Arch Linux
- Riced Hyperland setup (matches laptop theme)
- Daily Driver Desktop

## Lab Hypervisor
- 2012 MacMini
- Proxmox
- Accessible via Tailscale
- Used for:
    - Classes when an isolated environment is needed
    - Running a project that I would like to use various devices to work on without replicating an environment
    - Experimenting with other OSes in a low risk environment
    - Used to run a DNS filter (PiHole)
    - Other expirements

## File Server
- 2012 Dell XPS 14 Laptop
- OpenMediaVault
- Accessible via Tailscale
- 1TB of storage
- Replaces cloud storage for a fraction of the cost and maintains data privacy



# Future Expansions
## Self Hosted Web Server
- Raspberry Pi 4B
    - Currently have this, it is just not in use
- Will allow me to self host my personal website for free and easily spin up preproduction/testing environments
- Need to subnet home network first for security

## Self Hosted AI Model
- *Tentative project*
- Still running numbers, but would like to have a newer, more powerful computer for running my own "ChatGPT" but trained exactly for my use cases (cheaper than paying subscriptions and data stays private)
