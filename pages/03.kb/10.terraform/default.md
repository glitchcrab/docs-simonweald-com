---
title: terraform
date: '16:48 09-05-2022'
published: true
cache_enable: true
visible: true
---

#### Importing Cloudflare records

- get record ID from Cloudflare API:

```
curl https://api.cloudflare.com/client/v4/zones/<zone_id>/dns_records \
    -H "X-Auth-Key:<api_key>" \
    -H "X-Auth-Email:<account_email>" \
    -H "Content-Type:application/json" \
    | jq .
```

- create the resource declaration in the terraform manifest.
- import the resource:

```
terraform import cloudflare_record.<resource_name> <zone_id>/<record_id>
```