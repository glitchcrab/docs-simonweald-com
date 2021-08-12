---
title: 'Cluster setup'
date: '09:17 12-08-2021'
taxonomy:
    category:
        - docs
published: true
routable: true
visible: true
---

Documentation on general configuration of Proxmox cluster nodes.

##### Nag dialog

Use [pve-nag-buster](https://github.com/foundObjects/pve-nag-buster) on each node to remove the nag dialog:

```bash
wget https://raw.githubusercontent.com/foundObjects/pve-nag-buster/master/install.sh -O /tmp/pve-nag-buster.sh
chmod +x /tmp/pve-nag-buster.sh
sudo /tmp/pve-nag-buster.sh
```

##### Package repo

```bash
echo "deb http://download.proxmox.com/debian/pve buster pve-no-subscription" \
	tee -a /etc/apt/sources.list.d/pve-no-subscription.list
```