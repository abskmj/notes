---
title: "Getting Started with Parcel.js"
date: 2021-05-05T18:00:08+05:30
tags: ['ParcelJS', 'Javascript', 'Bundler']
---

# Steps
- Install NPM module
```
npm install --save-dev parcel-bundler
```

- Add NPM scripts
```json
{
  "scripts": {
    "start": "parcel index.html",
    "build": "parcel build index.html"
  }
}
```

- Start the development server
```
npm start
```

# Bonus
- Set the public url
```json
{
  "scripts": {
    "build": "parcel build index.html --public-url ./"
  }
}
```