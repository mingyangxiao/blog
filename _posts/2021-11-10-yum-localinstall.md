---
layout: post
title: Yum 下载安装包及对应依赖包
excerpt: Yum 下载安装包及对应依赖包
cover: /assets/img/yum.png
tags: Linux Yum
---

#### 简介

通常生产环境由于安全原因都无法访问互联网。此时就需要进行离线安装，主要有两种方式：源码编译、rpm包安装。源码编译耗费时间长且缺乏编译环境，所以一般都选择使用离线 rpm 包安装。

#### 方案一（推荐）：repotrack

```bash
# 安装yum-utils
$ yum -y install yum-utils

# 下载 python3 全量依赖包
$ repotrack python3
```

####  方案二：yumdownloader

```bash
# 安装yum-utils
$ yum -y install yum-utils

# 下载 python3 依赖包
$ yumdownloader --resolve --destdir=/tmp python3
```

参数说明：

- —destdir：指定 rpm 包下载目录（不指定时，默认为当前目录）。
- —resolve：下载依赖的 rpm 包。

**注意** ：仅会下载主软件包和基于你现在的操作系统所缺少的依赖关系包。

#### 方案三：yum  downloadonly 插件

```bash
# 安装插件
$ yum -y install yum-download

# 下载 python3 依赖包
$ yum -y install python3 --downloadonly --downloaddir=/tmp
```

参数说明：

- —downloaddir：指定 rpm 包下载目录（不指定时，默认为当前目录）。
- —downloadonly：仅下载rpm包。

**注意** ：仅会下载主软件包和基于你现在的操作系统所缺少的依赖关系包。

####  离线安装 rpm

```bash
rpm -ivh *.rpm 
#或
yum -y localinstall * 
```

