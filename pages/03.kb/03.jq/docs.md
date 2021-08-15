---
title: jq
published: true
taxonomy:
    category:
        - docs
---

# JQ

* piping jq to less with colour:

```bash
jq -C . data.json |less -R
```

* piping streaming output to jq:

```bash
(echo 'asdf {"type":"stats"}'; sleep 1 ) | cut -f 2 -d ' ' | jq --unbuffered .
```

* loop over dict and get list of item keys which match a pattern:

```bash
kubectl get secret secretname -n namespace -o json \
  | jq -r '.metadata.annotations | with_entries(select(.key|match("certmanager.k8s.io")))' \
  | jq -r '. | keys[]'
```