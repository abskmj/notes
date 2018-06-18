---
title: "Using a remote repository with Glitch.com"
date: 2018-06-18T11:25:57Z
tags: ["Tutorial","Glitch.com","Git"]
---

[Glitch](https://glitch.com/) is a online workspace that support javascript for development with live previews.

A gitch project already has a local git repository that adds remix and review functionality. Each of the changes done to the code is automatically committed to this repository. Hence, one should NOT connect to a remote to this repository. If done, there will be unnecessary checkpoint commits in the remote repository as well when pushed.

Rather, a separate git repository can be set using the current project as working directory.

## Create a separate local Git repository
- Create a folder for this new git repository.
```bash
mkdir .git-remote
cd .git-remote
```

- Initialize an bare git repository.
```bash
git init --bare
```

- Add the remote repository
```bash
git remote add orgin {{remote_git_url}}
```

## Using new Git Repository
- All the git comands can be used by point the git directory to the new repository.
```bash
git --git-dir=".git-remote" {{git_options}}
```

- Commits:
```bash
git --git-dir=".git-remote" commit -am "new commit"
```

- Push/Pull:
```bash
git --git-dir=".git-remote" push origin master
```

## Adding an Alias
- An alias can be added to glitch console by creating a `.bash_profile` file in project root and adding:

```bash
alias rgit=git --git-dir=".git-remote"
```

- Alias can be used:

```bash
rgit commit -m "new commit"
```