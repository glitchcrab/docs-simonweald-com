---
title: grep
published: true
taxonomy:
    category:
        - docs
---

* grep for $string1 AND $string2:

```bash
grep -RiE 'rabbit.*guest' /etc/*
```

* diff files and show only common lines:

```bash
$ grep -F -x -f file1 file2
```