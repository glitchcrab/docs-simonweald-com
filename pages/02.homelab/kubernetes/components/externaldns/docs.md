---
title: external-dns
taxonomy:
    category:
        - docs
published: true
visible: true
---

##### 

Kubernetes clusters in my homelab aren't automatically exposed externally, therefore I need to point externally-accessible domains to my home IP address.

This can be achieved using the `external-dns.alpha.kubernetes.io/target` annotation to Ingress resources. Assuming you have a dynamic DNS record of `ingress.lab.domain.com` which points to your home IP, annotate Ingresses which you wish to be exposed to the internet like the example below. This will create a CNAME of `my.internal.service.domain.com` which points to `ingress.lab.domain.com`.

```yaml
metadata:
  annotations:
    external-dns.alpha.kubernetes.io/target: ingress.lab.domain.com
...
spec:
  rules:
  - host: my.internal.service.domain.com
```

```bash
dig a my.internal.service.domain.com +short
ingress.lab.domain.com.
81.111.11.71
```