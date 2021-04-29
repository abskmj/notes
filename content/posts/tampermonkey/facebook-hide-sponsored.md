---
title: "TamperMonkey Script to hide Facebook Sponsored Posts"
date: 2021-04-29T08:42:07+05:30
tags: ['TamperMonkey', 'Facebook', 'JavaScript']
---

This TamperMonkey script hides sponsored posts on the Facebook feed.

```javascript
// ==UserScript==
// @name         Hide Sponsored Posts on Facebook
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  Hide Sponsored Posts on Facebook
// @author       abskmj@gmail.com
// @match        https://www.facebook.com
// @grant        none
// @require      https://cdnjs.cloudflare.com/ajax/libs/arrive/2.4.1/arrive.min.js
// ==/UserScript==

const isSponsored = (article) => {
    let text = '';

    article.querySelectorAll('a[href="#"] > span[aria-labelledby] > span > span').forEach((span) => {
        if (!span.getAttribute('style')) text += span.textContent
    })

    return text.toLowerCase().includes('ponsored')
}

const checkAndHide = (article) => {
    if (isSponsored(article)) {
        console.log('Hiding a sponsored post')
        article.style.display='none'
    }
}

const start = async () => {
    try {
        console.log('Start TamperMonkey Script')

        document.arrive('[role=article]', function () { checkAndHide(this) });
        document.querySelectorAll('[role=article]').forEach((article) => { checkAndHide(article) })
    } catch (err) {
        console.error('TamperMonkey Script Error:', err)
    }
}

start()
```
