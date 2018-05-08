---
title: "Custom Model Methods in Loopback"
date: 2018-05-07T08:44:22Z
tags: ["Tutorial","Loopback","Model","Remote Method"]
---

Loopback models can be extended by adding custom methods to them. A method can be:  

- Model Method: the method is available on Model itself.
- Instance Method: the method is available on an instance of the model.


# Model JS file
```javascript
// Model.js
module.exports = function(Model) {

  // Model Method
  Model.method = function() {
    ...
  }
  
  // Instance Method
  Model.prototype.method = function() {
    ...
  }
}
```

```javascript
// Model method
var Model = app.models.Model;
Model.method();

// Instance Method
var instance = new Model();
instance.method();
```