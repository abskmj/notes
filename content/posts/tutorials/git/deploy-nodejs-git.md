---
title: "Deploy a NodeJS application using Git"
date: 2018-05-09T05:09:36Z
tags: ["Tutorial","Hugo","Git","Deployment","Git Hook"]
---

# Remote Repository on Deployment Server

Create two folders named `project.git` and `project.source`. Create a bare git repo in `project.git`
```
git init --bare
```

Configure `project.source` as working folder for source code by adding below to `project.git/hooks/post-receive`
```
#!/bin/sh
git --work-tree=/<path>/project.source --git-dir=/<path>/project.git checkout -f
```

Change file persion to `755` to make it executable.
```
chmod 755 project.git/hooks/post-receive
```

Add a remote to local repo
```
git remote add dev git+ssh://user@server/projects/ppe_mc/ppe.git
```

Above steps are generic to any kind of project as it simply transfers the code to the server. The latest version of the source code will be available in the working folder after each push.
```
git push dev master
```

# Deployment using Hooks
Steps to install dependencies, build, test, deploy can be added to the `post-receive` hook script which will be executed every time the source code is pushed.

```
#!/bin/sh
git --work-tree=/<path>/project.source --git-dir=/<path>/project.git checkout -f

# Steps to build and deploy nodejs application
cd /<path>/project.source
npm install
npm run build
pm2 restart node_app
```