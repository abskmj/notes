---
title: "Setup a Public Samba Share"
date: 2020-07-10T16:59:31+05:30
tags: ["WD MyCloud", "Debian", "Jessie", "Samba", "Share"]
---

# Install Samba
```bash
apt-get install samba
```

# Configure Samba
Below configuration will create a new samba share which can be accessed by anybody on the network without entering any credentials.

```bash
nano /etc/samba/smb.conf
```

Contents of `smb.conf`
```
[global]
workgroup = WORKGROUP
server string = Samba Server %v
netbios name = WDMyCloud
security = user
map to guest = bad user
dns proxy = no

[Public]
   path = /data/shares/Public
   force group = users
   create mask = 0660
   directory mask = 0771
   browsable =yes
   writable = yes
   guest ok = yes
```

# Restart Samba Service
The samba service has to restarted each time to use the new configuration.
```bash
/etc/init.d/samba restart
```