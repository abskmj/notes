---
title: "Registering Custom Remote Methods in Loopback"
date: 2018-01-31T19:44:51+05:30
draft: true
---

# Remote Methods
Remote methods in loopback are custom APIs that can be defined on models to fulfill custom requirements other than the default set of CRUD APIs available in loopback.

# Static vs Instance Remote Methods
Static remote methods are referenced on the Model itself where as instance remote methods are referenced on a model instance.

```
// static
POST /model/custom

// instance
POST /model/{id}/custom
```