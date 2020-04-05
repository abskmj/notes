---
title: "Sources List for Debian Wheezy"
date: 2020-04-05T18:26:32+05:30
tags: ["WD MyCloud", "Debian", "Wheezy" , "apt-get"]
---

> As Debian wheezy version has reached the end of life, the usual repositories do not exist anymore and have been moved to the archive.

- Open `/etc/apt/sources.list`

- Comment existing sources
- Add below sources

```bash
deb http://archive.debian.org/debian/ wheezy main non-free contrib
deb-src http://archive.debian.org/debian/ wheezy main non-free contrib
```

- Now you can run
```bash
apt-get update
```

- If you get below error
```bash
There is no public key available for the following key IDs
```

- Install below package
```bash
apt-get install debian-archive-keyring
```

- Now you can rerun
```bash
apt-get update
```