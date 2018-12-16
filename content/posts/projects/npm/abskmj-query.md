---
title: "NPM Module - Complex JSON to Query String"
date: 2018-10-17T06:38:37Z
tags: ["Project","NPM","NodeJS"]
---

# [@abskmj/query](https://www.npmjs.com/package/@abskmj/query)
It is an NPM module that converts complex JSON with arrays and nested objects into URL parameters or query string. It can also parse such query string back to JSON. 

## Example
```javascript
const query = require('@abskmj/query');

// query to get a list of 10 people between age 17 and 66, sorted by their age 

let filters = {
    where: {
        age: { $gt: 17, $lt: 66 },
    },
    options: {
        limit: 10,
        sort: { age: -1 }
    }
}

const queryString = query.stringify(filters);

console.log(queryString);

/*
console:
where[age][$gt]=17&where[age][$lt]=66&options[limit]=10&options[sort][age]=-1
*/


const json = query.parse(queryString);

console.log(JSON.stringify(json, null, 2));

/*
console:
{
  "where": {
    "age": {
      "$gt": 17,
      "$lt": 66
    }
  },
  "options": {
    "limit": 10,
    "sort": {
      "age": -1
    }
  }
}
*/
```


# Motivation
I have been working on lots of MEVN/MEAN stack applications lately. I thought it would a great idea to write the mongoose queries in the front-end code rather than creating multiple APIs for different queries. It saves lots of effort on the backend code.