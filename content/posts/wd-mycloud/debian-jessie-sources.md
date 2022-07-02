---
title: "Sources List for Debian 8 (Jessie)"
date: 2022-07-02T00:00:00+05:30
tags: ["WD MyCloud", "Debian", "Jessie" , "apt-get"]
---

> Debian 8 has been superseded by Debian 9 (stretch). Regular security support updates have been discontinued as of June 17th, 2018. Jessie also benefits from Long Term Support (LTS) until the end of June 2020. The LTS is limited to i386, amd64, armel and armhf.

- Open `/etc/apt/sources.list`

- Comment existing sources
- Add below sources

```bash
deb http://deb.debian.org/debian jessie main contrib non-free
deb-src http://deb.debian.org/debian jessie main contrib non-free

deb http://deb.debian.org/debian-security/ jessie/updates main contrib non-free
deb-src http://deb.debian.org/debian-security/ jessie/updates main contrib non-free

deb http://deb.debian.org/debian jessie-updates main contrib non-free
deb-src http://deb.debian.org/debian jessie-updates main contrib non-free
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