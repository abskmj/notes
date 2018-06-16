---
title: "Authenticate REST APIs using JWT"
date: 2018-05-08T10:41:21Z
tags: ["Topic","REST APIs","JWT","Authentication","Security"]
---

# Authentication vs Authorization

- Authentication: identifying the user who is accessing the resource
- Authorization: checking if the user has permission to perform an action on the resource (e.g updating the resource)


# JWT for Authentication
JWT or JSON Web Token is a preferrable method for authenticating REST APIs because:  

- A datastore is not required for its verification.
- It can be issued and verified by a specific application server which has access to the `secret` key.
- It has placeholder for additional data whose integrity can be validated.
- It has an expiry time associated with it.

JWT can be passed in the `Authorization` header.

# JWT not for Authorization
The data placeholder in JWT makes it a candidate for authorization as well. Server can put roles/grants information in it. However, it is not recommended to be used because:

- It is difficult to update a JWT.
- It is difficult to revoke a JWT.

Any changes to JWT is not real-time as each has a specified time of expiry before which it is treated as valid by the application server.