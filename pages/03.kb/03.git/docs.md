---
title: git
date: '13:03 14-03-2022'
taxonomy:
    category:
        - docs
---

Move commits accidentally committed to `main` onto a feature branch:

```
git checkout main
git checkout <commit hash prior to the first one to move>
git checkout -b feature_branch
git rebase main
# or
git cherry-pick <commit hashes to move>
git checkout main
git reset --hard <commit hash used to create initial branch>
```