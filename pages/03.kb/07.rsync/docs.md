---
title: rsync
date: '12:56 15-08-2021'
taxonomy:
    category:
        - docs
---

* rsync saving ACLs and xattrs:

```bash
rsync -avPAX
```

* rsync only files less than $x days old preserving directory path on remote host:

```bash
find . -type f -mtime -4 -print0 | rsync -0adv --files-from=- ./ root@target-host:/target/path/
```

* rsync files created in the last 30 days:

```bash
rsync -avP --files-from=<(find . -type f -mtime -30 -exec basename {} \;) `pwd`/ root@target:/path/
```

* rsync a filesystem and tar it at the destination:

```bash
tar --numeric-owner --one-file-system -cvf - . | ssh root@target "cat > /output/file.tar"
```

* rsync with spaces in path (-s = protect-args):

```bash
rsync -avPs root@target:/path/to/'a file' /destination/
```

* rsync full system backup:

```bash
rsync -chavzP --rsync-path="sudo rsync" --stats --exclude /dev/ --exclude /proc/ user@source:/ .
```

* rsync only selected directories:

```bash
rsync -avP --include 'dir1/***' --include 'dir2/***' --exclude '*' /tmp/test/ root@remote:/tmp/test/
```
