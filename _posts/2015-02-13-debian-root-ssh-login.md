---
layout: post
title: Debian/Ubuntu开启root账户远程SSH登陆
tags: Linux Debian Ubuntu
---



Debian/Ubuntu 安装完后，默认是禁止root账户远程登陆的，需要通过修改配置文件实现root账户远程登陆。

```shell
vi /etc/ssh/sshd_config
```

查找   `PermitRootLogin`

```shell
PermitRootLogin without-password
```

修改为

```shell
PermitRootLogin yes
```

重启ssh服务

```shell
service ssh restart
```



