---
title: "Developing and Angular project on Cloud9 IDE"
date: 2018-07-10T12:46:13Z
tags: ["Angular", "Node.js", "NPM" , "Tutorial", "Cloud9 IDE"]
---

## Update NodeJS version
- All of the blank VMs on cloud9 have [nvm](https://github.com/creationix/nvm) pre installed.
- List all the available versions from [the official site](https://nodejs.org).

```bash
nvm ls-remote
```

- Choose to install the latest version

```bash
nvm install v10.6.0
```

- Choose to use the latest version

```bash
nvm use v10.6.0
```

- Check the version in use

```bash
node --version
```


## Angular
- Install latest [Angular CLI](https://cli.angular.io/) package

```bash
npm install -g @angular/cli
```

- Create a new project named `my-project` (you can use any name you need)

```bash
ng new my-project
cd my-project
```

- Change `start` script in `package.json`

```json
{
  ...
  
  "scripts": {
    ...
    
    "start": "ng serve --host $IP  --port $PORT --public-host $C9_HOSTNAME",
    
    ...
  }
  
  ...
}

```

- On IDE menu, click on `Preview > Preview Running Application` to get the preview URL.

## Downside
Everything works perfectly expect that the live reload, sometimes, is slower than usual.