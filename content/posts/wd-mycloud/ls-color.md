---
title: "Turn off the color with ls command"
date: 2020-05-01T10:05:46+05:30
tags: ["WD MyCloud", "Debian", "Jessie"]
---

# Alias
See if there are any alias defined for `ls` on your terminal

```bash
alias
```

For me it was `alias ls='ls $LS_OPTIONS'` and `LS_OPTIONS` environment variable had a value of `--color=auto`

# .bashrc
Check the contents of your `~/.bashrc` file. Generally, these aliases are defined here. Mine had these lines

```
export LS_OPTIONS='--color=auto'
eval "`dircolors`"
alias ls='ls $LS_OPTIONS'
alias ll='ls $LS_OPTIONS -l'
alias l='ls $LS_OPTIONS -lA'
```

Update `export LS_OPTIONS='--color=auto'` to `export LS_OPTIONS='--color=never'` and restart the terminal

```
export LS_OPTIONS='--color=never'
eval "`dircolors`"
alias ls='ls $LS_OPTIONS'
alias ll='ls $LS_OPTIONS -l'
alias l='ls $LS_OPTIONS -lA'
```

Also, take note of the other two helpful aliases.