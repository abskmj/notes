---
title: "Setup Aria2 Download Utility on Debian"
date: 2022-07-02T00:00:00+05:30
tags: ["WD MyCloud", "Debian", "Jessie", "Aria2"]
---

There may be other ways to install the Aria2 download utility on Debian, but this is what I follow on my almost 10 years old network hard disc device which runs on Debian 8 (Jessie).

> [aria2](https://aria2.github.io/) is a lightweight multi-protocol & multi-source command-line download utility. It supports HTTP/HTTPS, FTP, SFTP, BitTorrent and Metalink. aria2 can be manipulated via built-in JSON-RPC and XML-RPC interfaces.

# Install Aria2
Get the latest Debian package for ARM architecture from [github.com](https://github.com/q3aql/aria2-static-builds/releases). For example, `aria2-1.36.0-linux-gnu-arm-rbpi-build1.deb`. You can choose the version and architecture according to your need and machine.

```bash
dpkg -i aria2-1.36.0-linux-gnu-arm-rbpi-build1.deb
```

# Create Configuration
Create a configuration file in the home directory. This configuration will be automatically picked up by `aria2c` executable. For example, `/root/aria2/aria.conf`.

```bash
#basic
dir=/data/shares/public/Downloads
max-concurrent-downloads=3
check-integrity=true
continue=true
input-file=/root/.aria2/aria2.session

#bittorrent
bt-enable-lpd=true
enable-dht=true
enable-peer-exchange=true
max-overall-upload-limit=1M
seed-time=0

#rpc
enable-rpc=true
rpc-listen-all=true

#advanced
daemon=true
disable-ipv6=true
max-overall-download-limit=5M
save-session=/root/.aria2/aria2.session
save-session-interval=60
```

# Start Aria2
```bash
aria2c
```