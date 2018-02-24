---
title: "Enable Destroy All API for a model in Loopback"
date: 2018-01-31T19:28:48+05:30
tags: ["Tutorial","Loopback","Model","Remote Method"]
---

Destroy All API (`Model.destroyAll()`) is, by default, disabled to avoid accidental bulk deletion of data. However, it might be required for developmental purposes.

# Remote Method
A corresponding remote method can be added to the `model.js` file to enable this API. This method also supports a filter to enable selective deletion.

```javascript
module.exports = function (Model) {
    Model.remoteMethod('destroyAll', {
        isStatic: true,
        description: 'Delete all matching records',
        accessType: 'WRITE',
        accepts: { arg: 'where', type: 'object', description: 'filter.where object' },
        http: { verb: 'del', path: '/' }
    });
};
```