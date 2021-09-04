---
title: networking
date: '22:52 02-09-2021'
taxonomy:
    category:
        - docs
published: true
routable: true
cache_enable: true
visible: true
---

#### instances

Instances use slices of `172.25.0.0/23`.

**infrastructure instances**

- `172.25.0.0/27`

| VM ID | IP               | instance          | notes                                               | config                                                                                           |
|----------|----------------|--------------------|------------------------------------------------|-------------------------------------------------------------------------------------|
| 200     | 172.25.0.3 | tailscale-relay | tailscale relay to access LAN           | https://github.com/glitchcrab/homelab-instance-tailscale-relay   |
| 201     | 172.25.0.4 | internal-infra   | misc infra uses (image building etc) | https://github.com/glitchcrab/homelab-instance-infra-conductor |

- `172.25.0.32/27` - unused

**kubernetes management cluster**

- `172.25.0.64/28`

| VM ID | IP                 | instance  | notes          |
|----------|------------------|-------------|-----------------|
| x         | 172.25.0.64 | master1 | master node |
| x         | 172.25.0.65 | master2 | master node |
| x         | 172.25.0.66 | master3 | master node |
| x         | 172.25.0.67 | worker1 | worker node |
| x         | 172.25.0.68 | worker2 | worker node |
| x         | 172.25.0.69 | worker3 | worker node |