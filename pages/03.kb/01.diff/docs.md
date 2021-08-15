---
title: diff
published: true
taxonomy:
    category:
        - docs
routable: true
visible: true
---

* Recursive diff between two file trees, ignoring any which don't exist on either side:

```bash
git diff --diff-filter=MR file1 file2
```

* or:

```bash
git diff --diff-filter=CMRTXB file1 file2
```

* Diff local and remote file:

```bash
diff foo <(ssh myServer 'cat foo')
```