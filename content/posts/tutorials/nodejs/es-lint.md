---
title: "Configure ES Lint with Airbnb rules for a Node.js Application"
date: 2019-07-01T20:15:18+05:30
tags: ["Tutorial","Nodejs","VSCode","Lint", "ESLint", "Airbnb"]
---

## Install ES Lint modules
```bash
npm install --save-dev eslint-plugin-import eslint
```

## Install Airbnb config
Use the base version for Node.js applications. They also publish a version for React applications as `eslint-config-airbnb`.
```bash
npm install --save-dev eslint-config-airbnb-base
```

## Config File
Create a `.eslintrc` file with following contents to Airbnb rules for the Node.js Application.
```json
{
    "extends": "eslint-config-airbnb-base"
}
```

## NPM Scripts
Create few npm scripts to integrate linting into development flow.
```json
{
    "scripts":{
        "start": "node .",
        "lint": "eslint --fix .",
        "dev": "nodemon --exec 'npm run lint && npm run start'"
    }
}
```

## VS Code
There is an extension on VS Code for ES Lint, available at https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint