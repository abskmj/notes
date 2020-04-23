---
title: "Git Info Variables on Hugo"
date: 2020-04-23T13:16:58+05:30
tags: ['Hugo', 'Git']
---

# Enable Git Info Variables
> Enable `.GitInfo` object for each page (if the Hugo site is versioned by Git). This will then update the `Lastmod` parameter for each page using the last git commit date for that content file.

## Terminal
```bash
hugo --enableGitInfo
```

## Config File
> Hugo uses the `config.toml`, `config.yaml`, or `config.json` (if found in the site root) as the default site config file.
> 
> The user can choose to override that default with one or more site config files using the command line `--config` switch.

```toml
enableGitInfo = true
```

# Dates on Hugo Pages
Once Git Info variables are enabled, Hugo updates only the `LastMod` parameter for each page which is not used in most of the themes. However, Front Matter configuration can be set in the config file to show the dates from git info.

> Dates are important in Hugo, and you can configure how Hugo assigns dates to your content pages. You do this by adding a frontmatter section to your `config.toml`.

```toml
[frontmatter]
date = [":git" ,"date", "publishDate", "lastmod"]
```