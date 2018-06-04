---
layout: post
title: Nginx https + Tomcat http 非80/443端口配置方式
excerpt: Nginx https + Tomcat http 非80/443端口配置方式
cover: /assets/img/tomcat.jpg
tags: 运维 Tomcat Nginx
---

Nginx 增加以下配置

```nginx
proxy_set_header Host               $host:$server_port; 
proxy_set_header X-Real-IP          $remote_addr;
proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
proxy_set_header X-Forwarded-Proto  $scheme;
```

Tomcat server.xml配置

```xml
<Engine name="Catalina" defaultHost="localhost">
  <Valve className="org.apache.catalina.valves.RemoteIpValve"
         remoteIpHeader="X-Forwarded-For"
         protocolHeader="X-Forwarded-Proto"
         protocolHeaderHttpsValue="https"  
         httpsServerPort="4433"/>
</Engine>
```