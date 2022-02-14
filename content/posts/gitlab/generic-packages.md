---
title: "Manage Generic Packages on Gitlab"
date: 2022-02-14T11:21:45+05:30
tags: ['Gitlab', 'Packages']
---

Generic packages on GitLab are a convenient way to manage project artifacts. It supports versioning. They can be pulled and used in other CI/CD pipelines too.

# Upload/Download a Package

- Upload

```bash
curl \
-u $user:$password \
--upload-file ./$package_name.zip \
https://gitlab.com/api/v4/projects/$project_id/packages/generic/$package_name/$package_version/$package_name.zip
```
- Download

```bash
curl \
-u $user:$password \
--output /$package_name.zip \
https://gitlab.com/api/v4/projects/$project_id/packages/generic/$package_name/$package_version/$package_name.zip
```

# Prerequisites

## Deploy Token
- Navigate to the `Settings > Repository > Deploy Tokens` section of the Gitlab repo to create a deploy token
- Set the username and use it as `$user`
- Select scopes `read_package_registry` and `write_package_registry`
- Create the token and use it as `$password`

## Project ID
- Navigate to repo home page
- `Project ID` is mentioned in the top header section, just below the repo name
- Use the value as `$project_id`