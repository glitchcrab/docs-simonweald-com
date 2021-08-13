---
title: SSH
date: '11:01 12-08-2021'
content:
    items: '@self.modular'
---

##### Force SSH to only use password auth

```
ssh -o PasswordAuthentication=yes -o PreferredAuthentications=keyboard-interactive,password -o PubkeyAuthentication=no
```

