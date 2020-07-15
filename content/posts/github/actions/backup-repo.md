---
title: "Backup Repository with a Github Action Workflow"
date: 2020-07-15T18:10:09+05:30
tags: ['Github', 'Actions', 'Workflow', 'Mirror', 'Backup', 'Git', 'Gitlab']
---

I always like to have a backup copy of all my important git repositories hosted on Github. I use a private repository at Gitlab to mirror each repository on Github. Currently, I have a Github Action workflow configured to copy it on any git push or any branches are deleted.

# Github Action Workflow
Create a `.github/workflows/mirror.yml` in the Github repository with the follow contents.

```yml
name: Mirror to Gitlab

on: [push, delete]

jobs:
  gitlab:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - uses: pixta-dev/repository-mirroring-action@v1
      with:
        target_repo_url:
          git@gitlab.com:<username>/<repository>.git
        ssh_private_key:
          ${{ secrets.GITLAB_SSH_KEY }}
```

# Credentials
Create an RSA key pair to allow Github action runner to write to the Gitlab repository.

```bash
ssh-keygen -t rsa -b 2048 -C "<comment>"
```

Executing the command will create two files, one with `.pub` extension which is the public key and one with no extension which is the private key. 

Since I like to use a different set of key pair for each repository, I

## Gitlab (Public Key)
Add a deploy key by navigating to `Repository > Settings > Deploy Keys > Expand > Add Key`. Fill the contents of `.pub` file or the public key here. Details at [docs.gitlab.com](https://docs.gitlab.com/ce/user/project/deploy_keys/).

> **IMPORTANT** - Remember to check `Write access allowed` option while adding the key

## Github (Private Key)
Add a secret by navigating to `Repository > Settings > Secrets > New Secret`. Fill the contents of the private key and name as `GITLAB_SSH_KEY`. Details at [docs.github.com](https://docs.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets).