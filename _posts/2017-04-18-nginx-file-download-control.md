---
layout: post
title: Nginx利用X-Accel-Redirect控制文件下载权限
excerpt: Nginx利用X-Accel-Redirect控制文件下载权限
tags: 开发 Nginx
---

```
location /download/ {
    internal;#将该路径标记为仅内部访问
    root   /some/path;
}
```

```java
String fileName = request.getParameter("fileName");
if (认证通过) {
    response.setHeader("Content-Type", "application/octet-stream");
    response.setHeader("Content-Disposition", "attachment;filename*=\"UTF-8''" + URLEncoder.encode(fileName, "UTF-8") + "\"");
    /*返回X-Accel-Redirect给Nginx*/
    response.setHeader("X-Accel-Redirect", "/download/" + URLEncoder.encode(fileName, "UTF-8"));
} else {
    response.sendError(403);
}
```
