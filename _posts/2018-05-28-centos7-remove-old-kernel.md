---
layout: post
title: CentOS删除旧内核
excerpt: CentOS删除旧内核
---

查看已经安装的内核

命令:

```
rpm -q kernel
``` 

结果:

```
kernel-2.6.32-279.14.1.el6.i686 
kernel-2.6.32-279.el6.x86_64
kernel-2.6.32-358.6.1.el6.x86_64
```


删除旧内核

方法一(逐个删除)
 
```
rpm -e kernel-2.6.32-279.14.1.el6.i686
``` 

方法二(需安装yum-utils)

```
sudo package-cleanup --oldkernels --count=1

# --count 需保留的内核数量
``` 
