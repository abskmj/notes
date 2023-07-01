---
title: "Setup Aria2 Download Utility on Debian"
date: 2023-07-01T00:00:00+05:30
tags: ["WD MyCloud", "Debian", "Jessie", "Aria2"]
---

There may be other ways to install the Aria2 download utility on Debian, but this is what I follow on my almost 10 years old network hard disc device which runs on Debian 8 (Jessie).

> [aria2](https://aria2.github.io/) is a lightweight multi-protocol & multi-source command-line download utility. It supports HTTP/HTTPS, FTP, SFTP, BitTorrent, and Metalink. aria2 can be manipulated via built-in JSON-RPC and XML-RPC interfaces.

# Install Aria2
Get the latest Debian package for ARM architecture from [github.com](https://github.com/q3aql/aria2-static-builds/releases). For example, `aria2-1.36.0-linux-gnu-arm-rbpi-build1.deb`. You can choose the version and architecture according to your need and machine.

```bash
dpkg -i aria2-1.36.0-linux-gnu-arm-rbpi-build1.deb
```

# Create Configuration
Create a configuration file in the home directory. This configuration will be automatically picked up by the `aria2c` executable. For example, `/root/aria2/aria.conf`.

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
# Android App for Remote Control
Since I use Aria2 on a headless device, I have enabled remote control over RPC and use [Aria2App](https://github.com/devgianlu/Aria2App), an open-source app on my Android phone.

# Download Completion Script
I generally download a lot of large-sized archive files using Aria2. These files take a good amount of time to be extracted because of the low specification of the device.

Aria2 allows configuring a bash script which is executed automatically every time a download is completed.

The below script checks for if the downloaded file is an archive file, either a zip or a rar file, and extracts it to a folder with the same name.

```bash
#!/bin/bash
# check for archive file
if [ "${3: -4}" == ".rar" ] || [ "${3: -4}" == ".zip" ] 
then
  7z x "$3" -o"${3%.*}"
  chmod 777 -R "${3%.*}" # optional folder permissions
fi
```

It uses the 7zip utility to extract the file which can be installed by executing the below command
```bash
sudo apt install p7zip-full p7zip-rar
```

Add the below line to the `aria2.conf` file
```
on-download-complete=/root/.aria2/dl-complete.sh
```