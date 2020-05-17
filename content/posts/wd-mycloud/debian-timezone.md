---
title: "Change Timezone in Debian"
date: 2020-05-17T13:44:55+05:30
tags: ["WD MyCloud", "Debian", "Timezone", "timedatectl"]
---

# Using timedatectl

## Current Timezone
```bash
$ timedatectl
```

## Set Timezone
```bash 
$ timedatectl set-timezone Asia/Kolkata
```

## List Timezones
```bash
$ timedatectl list-timezones
$ timedatectl list-timezones | grep -i kolkata 
```