---
title: "Install Debian Jessie on WD MyCloud (Gen1)"
date: 2020-04-15T14:33:04+05:30
tags: ["WD MyCloud", "Debian", "Jessie"]
---

# De-attach WD Drive
- You will have to open your WD MyCloud device and remove the HDD or drive inside it. 
- Attach the drive to your computer.
- If you don't have a Linux based OS installed on your computer, you can boot your computer through a live USB. See how to create one at [ubuntu.com](https://ubuntu.com/tutorials/tutorial-create-a-usb-stick-on-windows#1-overview)

# Create Partitions
You can skip this section if you have not formatted the drive after connecting it to your computer and have the original partitions.

- Install need software
```bash
apt-get install parted
```

- Find your WD drive on your computer, look at the partition sizes and find the one that has simar size as your WD MyCloud. For me, it was `/dev/sdb` with a size around 1.8 TB.

```bash
fdisk -l
```

- Run the utility on your WD drive
```bash
parted /dev/sdb
```

- Print all partitions on the drive
```bash
print
```

- Remove all the partitions. For me, there was only one partition
```bash
remove 1
```

- Recreate all needed partitions
```bash
mklabel gpt
mkpart primary 528M 2576M
mkpart primary 2576M 4624M
mkpart primary 16M 528M
mkpart primary 4828M 100%
mkpart primary 4624M 4724M
mkpart primary 4724M 4824M
mkpart primary 4824M 4826M
mkpart primary 4826M 4828M
set 1 raid on
set 2 raid on
```
- Quit the utility
```bash
quit
```

- Format data and swap partitions
```bash
mkfs -t ext4 /dev/sdb4
mkswap /dev/sdb3
```

# Install Debian
- Find your WD drive on your computer, look at the partition sizes and find the one that has simar size as your WD MyCloud. For me, it was `/dev/sdb` with a size of around 1.8 TB.

```bash
fdisk -l
```
- Install software for RAID devices

```bash
apt-get install mdadm
```
- Mount RAID partitions

```bash
mdadm --stop /dev/md*
mdadm -A /dev/md0 /dev/sdb1 /dev/sdb2
```

- Mount data partitions

```bash
mount -t ext4 /dev/sdb4 /mnt
cd /mnt
```

- Download Clean Debian package and extract it

```bash
wget https://github.com/abskmj/wd-mycloud-gen1/releases/download/packages/clean-debian-jessie.tgz

tar -xvfz clean-debian-jessie.tgz
```
> If you are planning to install one of the original packages. You can download that package instead of Debian.
> 
> ```bash
> # v3.x
> wget https://github.com/abskmj/wd-mycloud-gen1/releases/download/packages/original-v03.04.01-230.tar.gz
> 
> tar -xvfz original-v03.04.01-230.tar.gz
> 
> # v4.x
> wget https://github.com/abskmj/wd-mycloud-gen1/releases/download/packages/original-v04.01.02-417.tar.gz
> 
> tar -xvfz original-v04.01.02-417.tar.gz
> ```

- Copy images to partitions

```bash
dd if=kernel.img of=/dev/sdb5
dd if=kernel.img of=/dev/sdb6
dd if=config.img of=/dev/sdb7
dd if=config.img of=/dev/sdb8
dd if=rootfs.img of=/dev/md0
```

# Re-attach WD Drive
- You can shut your computer down and remove the WD drive.

- You don't have to assemble the device completely right now, you can simply connect the plate to the drive and attach a LAN / power cord to it.

- It should start up and show a yellow light.
- You should see a green light in a while, which means Debian has started properly.
- You can now ssh into your MyCloud device.
```bash
ssh root@192.168.X.XXX # replace with your IP 
```

- The default password for the root user is `mycloud`.

- DO WHATEVER YOU WANT WITH YOUR NEW LINUX BOX! : )

> WARNING: Executing `apt-get upgrade` sometimes bricks the device and should avoid it.

#### References
- Original materials from fox-exe at [fox-exe.ru](https://fox-exe.ru/WDMyCloud/WDMyCloud-Gen1/)
- Re-uploaded packages at [github.com](https://github.com/abskmj/wd-mycloud-gen1/releases)