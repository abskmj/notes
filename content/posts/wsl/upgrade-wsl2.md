---
title: "Upgrade to WSL2"
date: 2021-05-19T21:30:00+05:30
tags: ["WSL", "Windows"]
---

Upgrade an existing version 1 WSL distro to version 2.

# Steps
- Open a power shell or cmd terminal
- List distros
```bash
wsl --list --verbose

# output
  NAME                   STATE           VERSION
* Ubuntu                 Running         1
```

- Upgrade to version 2
> Upgrade can take up to 15 minutes
```bash
wsl --set-version <distro-name> 2

# example
wsl --set-version Ubuntu 2
```

- Check if the upgrade was successful
```bash
wsl --list --verbose

# output
  NAME                   STATE           VERSION
* Ubuntu                 Running         2
```