---
title: "Enable Hibernate on Pop OS"
date: 2020-07-26T20:17:30+05:30
tags: ["PopOS","Hibernate","Ubuntu","Linux"]
summary: " "
---

# Prerequisites
## Check if the kernel supports Hibernation
```bash
cat /sys/power/state
```
It should list `disk` as an option on the list

## Check if a Swap file or partition is available
```bash
free -h
```
If `Swap` is listed as 0, it means a swap is not available and needs to be created.

# Create a Swap file
- Create a swap file.
```bash
sudo fallocate -l 6G /swapfile
```
`6G` can be updated with a recommended swap size for the machine which is listed under `How much swap do I need?` section at [help.ubuntu.com](https://help.ubuntu.com/community/SwapFaq)

- Permissions
```bash
sudo chmod 600 /swapfile
```

- Format as swap
```bash
sudo mkswap /swapfile
```

- Activate the swap
```bash
sudo swapon /swapfile
echo '/swapfile none swap defaults 0 0' | sudo tee -a /etc/fstab
```

# Configure Hibernation

## Swap UUID
Get the UUID for the swap file
```bash
findmnt -no UUID -T /swapfile
```
It looks something like below
```
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

## Swap offset
This is only needed when a swap file is available. Get the offset
```bash
sudo filefrag -v /swapfile | awk '{ if($1=="0:"){print $4} }'
```

It looks something like below
```
9999999..
```

## Update Kernel Options
```bash
sudo kernelstub -a “resume=UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx resume_offset=9999999”
```

Add below line to `/etc/initramfs-tools/conf.d/resume`. Create the file if not present
```
resume=UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx resume_offset=9999999
```

Update the configurations
```bash
sudo update-initramfs -u
```

# Test Hibernation
Remember to save your work before trying this out
```bash
sudo systemctl hibernate
```

# References
- SwapFaq at [help.ubuntu.com](https://help.ubuntu.com/community/SwapFaq)
- Guide to hibernate? [pop-planet.info](https://pop-planet.info/forums/threads/guide-to-hibernate-answer-is-a-guide.426/)