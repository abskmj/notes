---
title: "SSH Tunnels for Local Development"
date: 2020-08-29T15:30:35+05:30
tags: ["SSH", "SSH Tunnel", "Port Forward", "Productivity"]
---

## Local Port Forwarding
A service running on specific port of the server is accessible on a specific port of the local machine.

## Example

```
+---------------------+                       +-----------------------+
|                     |                       |                       |
|  +---------------+  |       SSH Tunnel      |  +-----------------+  |
|  |               |  <-----------------------+  |                 |  |
|  | mongodb:27017 |  |                       |  | localhost:27018 |  |
|  |               |  +----------------------->  |                 |  |
|  +---------------+  |      27017:27018      |  +-----------------+  |
|                     |                       |                       |
+---------------------+                       +-----------------------+
        Server                                          Local
```

Let's assume a MongoDB service is running on the server on port `27017` and is not accessible outside of the server. There is an application running the local machine and needs to connect to the MongoDB service running on the server.

With the below SSH tunnel, the MongoDB service is available on port `27018` of the local machine and accessible at `mongodb://127.0.0.1:27018/dev` for the application

```bash
ssh -L localhost:27018:localhost:27017 -N root@10.17.15.53
```

```
-L
  Specifies that the given port on the local (client) host is to be forwarded to the given host andport on the remote side.

-N
  Do not execute a remote command.
```

```
localhost:27018:localhost:27017
bind address of local machine : port of local machine : bind address of server : port of server
```