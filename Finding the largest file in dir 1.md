---
title: Finding the largest file in dir
notetype: feed
date: 12-06-2025
---

The below command will list all the files and directories inside of `/tmp` sorted by their size

```
du -h /tmp --max-depth=1 | sort -hr | head -n 20
```
