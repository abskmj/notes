---
title: "Working with Git Stash"
date: 2019-06-14T12:49:55+05:30
tags: ["Tutorial","Git","Git Stash", "Cheatsheet"]
---

Git stash is a great set of commands while working on volatile porjects where you are just trying out a proof of concept or a module.

## Save the local changes in Stash
```bash
git stash push -m {{ commit message}}
// example
git stash push -m {{ new logging module }}
``` 

## List all the change sets in Stash
```bash
git stash list
```

## Apply a change set from Stash
```bash
git stash apply {{ index }}
//example
git stash apply 1
```

> Not specifying an index with automatically apply first index

## Delete a change set without applying from Stash
```bash
git stash drop {{ index }}
// example
git stash drop 1
```
> Not specifying an index with automatically drop first index