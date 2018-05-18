---
title: "Set Proxy for Maven"
date: 2018-05-18T10:54:22Z
tags: ["Tutorial","Maven","Proxy"]
---

Proxy settings can be changed in `{{maven_installation_folder}}/conf/settings.xml`. Un-comment and change the values in `proxies` section of the file. Changes to this file doesn't require maven restart.

```xml
...

<proxies>
    <!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
     |-->
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username></username>
      <password></password>
      <host>{{proxy_host_or_ip}}</host>
      <port>8080</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    
</proxies>

...
```