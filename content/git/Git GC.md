---
title: Git GC
---

This note is about reducing our git repo size

1. Check repo size

```sh
git count-objects -vH
```

2. Clean Unused Object

Limit Git's memory usage

```bash
# Suggest config for Macbook Pro M1 16GB RAM
git config --global pack.windowMemory "512m"
git config --global pack.packSizeLimit "1g"
git config --global pack.threads "4"
```

Run garbage collection to remove dangling objects

```bash
git gc --prune=now --aggressive
```