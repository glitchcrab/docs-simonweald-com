---
title: vault
date: '23:18 04-09-2021'
taxonomy:
    category:
        - docs
published: true
routable: true
visible: true
---

##### policies

- assign policy `foo` to github team `admins`:

```bash
vault write auth/github/map/teams/admins value=foo
```

- assign policy `foo` directly to a user in the configured organisation:

```bash
vault write auth/github/map/users/glitchcrab value=foo
```

- assign multiple policies to github team `admins`:

```bash
vault write auth/github/map/teams/admins value=foo,bar
```