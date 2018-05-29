---
layout: post
title: EPEL源Nginx升级到官方最新版时遇到的问题及解决办法
excerpt: EPEL源Nginx升级到官方最新版时遇到的问题及解决办法
---



在一次升级nginx 版本中遇到的问题。

原本nginx直接使用 `yum install nginx` 安装的。后期想直接升级到官方最新版。

第一步:配置repo

```
vim /etc/yum.repos.d/nginx.repo
```

添加以下内容

```
[nginx]
name=nginx repo
baseurl=https://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

注意baseurl 中的7为centos 的主版本号 请根据实际情况修改

第二步：更新

```
yum update nginx
```

第三部：重启

```
systemctl restart nginx
```

发现重启失败，查看状态

```
systemctl status nginx
```

有以下提示：

```
nginx: [emerg] module "/usr/lib64/nginx/modules/ngx_http_geoip_module.so" version 1012002 instead of 1014000 in /usr/share/nginx/modules/mod-http-geoip.conf:1
```

这个原因是因为以前nginx modules和现在官方的modules不匹配，需要我们先将旧的modules卸载安装新版官方的modules。

命令如下：

```
yum remove nginx-mod*

yum install nginx-module-*
```

再次重启，故障解决。
