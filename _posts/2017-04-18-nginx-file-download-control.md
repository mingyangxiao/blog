---
layout: post
title: Nginx利用X-Accel-Redirect控制文件下载权限
excerpt: Nginx利用X-Accel-Redirect控制文件下载权限
cover: /assets/img/kb-big.jpg
tags: 开发 Nginx

---

在nginx配置文件中添加

```nginx
location /download/ {
    internal;#将该路径标记为仅内部访问
    root   /some/path;
}
```

后台处理

```java
// download.action

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

前端使用

```shell
dowload.action?fileName=test.txt
```
