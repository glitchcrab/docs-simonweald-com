---
title: cilium
taxonomy:
    category:
        - docs
published: true
routable: true
visible: true
---

#### BGP configuration

Now Cilium can speak BGP, it can be used to add routes to Services of type `Loadbalancer`:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: bgp-config
  namespace: kube-system
data:
  config.yaml: |
    peers:
      - peer-address: 172.25.0.1
        peer-asn: 65401
        my-asn: 65400
    address-pools:
      - name: default
        protocol: bgp
        addresses:
          - 172.27.0.1-172.27.0.254
```