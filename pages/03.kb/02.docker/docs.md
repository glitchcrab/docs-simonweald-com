---
title: docker
date: '20:16 30-08-2021'
taxonomy:
    category:
        - docs
published: true
---

**Run commands in a container's netns**

First get the container's ID from `docker ps`, then use it to get the PID:

```bash
pid=$(docker inspect -f '{{.State.Pid}}' ${container_id})
```
Ensure the netns dir exists and then create the required symlink:

```
mkdir -p /var/run/netns/
ln -sfT /proc/<pid>/ns/net /var/run/netns/<container id>
```

Run a command inside the netns:

```
ip netns exec <container id> ip a
```