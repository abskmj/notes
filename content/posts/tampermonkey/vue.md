---
title: "Use Vue.js in a TamperMonkey Script"
date: 2020-09-20T07:35:57+05:30
tags: ['TamperMonkey', 'Vue.js', 'JavaScript']
---

> [Vue.js](https://vuejs.org/) makes handling dynamic content easy in a [TamperMonkey](https://www.tampermonkey.net/) script.

# Include the script
Configure the script to include the Vue.js bundle from a CDN. 
```
// @require      https://cdn.jsdelivr.net/npm/vue
```
# Initialize a Vue.js App
It is recommended to initialize the Vue.js app after the page is ready.

```javascript
window.addEventListener("load", (event) => {
    // initialize app
    const app = new Vue({
      el: '#main-content',
      data: {}
      methods: {},
      template: ``
    })
})
```
