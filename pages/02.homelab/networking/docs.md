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

- `172.25.0.64/27`

| VM ID | IP                 | instance  | notes           |
|----------|------------------|-------------|------------------|
| -          | 172.25.0.64 | -              | haproxy VIP |
| 300     | 172.25.0.65 | haproxy1 | haproxy lb    |
| 301     | 172.25.0.66 | haproxy2 | haproxy lb   |
| 302     | 172.25.0.67 | haproxy3 | haproxy lb   |
| 303     | 172.25.0.68 | master1  | master node  |
| 304     | 172.25.0.69 | master2  | master node  |
| 305     | 172.25.0.70 | master3  | master node  |
| 306     | 172.25.0.71 | worker1  | worker node  |
| 307     | 172.25.0.72 | worker2  | worker node  |
| 308     | 172.25.0.73 | worker3  | worker node  |


**kubernetes management cluster (ClusterAPI/BYOH**

- `172.25.0.160/27`

| VM ID | IP                  | instance  | notes           |
|----------|-------------------|-------------|------------------|
| -          | 172.25.0.160 | -              | haproxy VIP |
| 330     | 172.25.0.161 | haproxy1 | haproxy lb    |
| 331     | 172.25.0.162 | haproxy2 | haproxy lb   |
| 332     | 172.25.0.163 | master1  | master node  |
| 335     | 172.25.0.166 | worker1  | worker node  |
| 336     | 172.25.0.167 | worker2  | worker node  |
| 337     | 172.25.0.168 | worker3  | worker node  |

### kubernetes service ranges

**overall range**

Kubernetes clusters use smaller slices of the following range:

- `172.27.0.0/24`

Individual clusters receive a `/27` of this range:

| Range                | BGP AS |cluster       |
|-----------------------|-------------|--------------|
| 172.27.0.0/27     | 65501 | k8s-mgmt |
| 172.27.0.32/27   | 65502 | |
| 172.27.0.64/27   | 65503 | |
| 172.27.0.96/27   | 65504 | |
| 172.27.0.128/27 | 65505 | |
| 172.27.0.160/27 | 65506 | |
| 172.27.0.192/27 | 65507 | |